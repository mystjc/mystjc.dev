<script>
  const phrases = [
    "Hello",
    "Hello there",
    "Greetings"
  ];

  function getRand() {
    let num = Math.floor(Math.random() * 3);
    return phrases[num];
  }
</script>

<div class="flex justify-center my-4">
  <span>{getRand()}</span>
</div>
