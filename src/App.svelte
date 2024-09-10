<script>
  import Scroll from "./Scroll.svelte";

  const urlQuery = new URLSearchParams(window.location.search);

  const duration = parseInt(urlQuery.get("duration"), 10) || 40;

  $: text = (() => {
    let txt = urlQuery.get("text");
    if (!txt) {
      return "Add your own text with ?text=yourtext\n If you want to decode base64 encoded text, add &decode=true\n\nAdjust speed with ?duration=durationInsSconds";
    }
    const decode = urlQuery.get("decode") === "true";
    console.log(decode);

    if (decode) {
      try {
        return atob(txt);
      } catch (error) {
        console.error(error);
      }
    }
    return txt;
  })();
</script>

<Scroll {duration}>
  {text}
</Scroll>
