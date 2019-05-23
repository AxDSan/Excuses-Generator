<script>
  function fallbackCopyTextToClipboard(text) {
    var textArea = document.createElement("textarea");
    textArea.value = text;
    document.body.appendChild(textArea);
    textArea.focus();
    textArea.select();

    try {
      var successful = document.execCommand("copy");
      var msg = successful ? "successful" : "unsuccessful";
      console.log("Fallback: Copying text command was " + msg);
    } catch (err) {
      console.error("Fallback: Oops, unable to copy", err);
    }

    document.body.removeChild(textArea);
  }
  function copyTextToClipboard(text) {
    if (!navigator.clipboard) {
      fallbackCopyTextToClipboard(text);
      return;
    }
    navigator.clipboard.writeText(text).then(
      function() {
        console.log("Async: Copying to clipboard was successful!");
      },
      function(err) {
        console.error("Async: Could not copy text: ", err);
      }
    );
  }

  function copyClickHandler() {
    copyTextToClipboard(
      document.getElementsByClassName("msg_container")[0].innerText
    );
  }
</script>

<style>
  .kc_fab_main_btn {
    width: 45px;
    height: 45px;
    border-radius: 100%;
    border: none;
    outline: none;
    color: #fff;
    font-size: 25px;
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
    transition: 0.3s;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
  }
</style>

<button class="kc_fab_main_btn btn-primary" on:click={copyClickHandler}><i class="far fa-copy"></i></button>
