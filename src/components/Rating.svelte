<script>
  const colourRange = [
    { start: 0, end: 4999, h: 220, s: 15, l: 35 },
    {
      start: 5000,
      end: 9999,
      h: 215,
      s: 60,
      l: 40,
    },
    {
      start: 10000,
      end: 14999,

      h: 225,
      s: 70,
      l: 50,
    },
    {
      start: 15000,
      end: 19999,

      h: 270,
      s: 60,
      l: 50,
    },
    {
      start: 20000,
      end: 24999,

      h: 310,
      s: 75,
      l: 55,
    },
    {
      start: 25000,
      end: 29999,

      h: 0,
      s: 80,
      l: 50,
    },
    {
      start: 30000,
      end: 99999,

      h: 45,
      s: 100,
      l: 50,
    },
  ];

  let { rating = 0 } = $props();

  const colour = $derived.by(() => {
    for (const range of colourRange) {
      if (rating >= range.start && rating <= range.end) {
        return range;
      }
    }

    return colourRange[0];
  });
</script>

<div class="rating" style="--h: {colour.h}; --s: {colour.s}%; --l: {colour.l}%">
  <div class="rating__bars">
    <div class="rating__bar"></div>
    <div class="rating__bar"></div>
  </div>

  <div class="rating__value">{new Intl.NumberFormat().format(rating)}</div>
</div>

<style>
  .rating {
    height: 80px;
    display: flex;
    transform: skewX(-8deg);
  }

  .rating__value {
    width: 180px;
    background-color: hsl(var(--h), var(--s), 35%);
    color: hsl(var(--h), var(--s), 95%);
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: border-box;
    border: 2px solid hsl(var(--h), var(--s), 35%);
    font-size: 2rem;
    font-family: "Rajdhani", sans-serif;
    font-weight: bold;
    letter-spacing: 2px;
  }

  .rating__bars {
    display: flex;
    gap: 3px;
  }

  .rating__bar {
    width: 10px;
    height: 100%;
    background-color: hsl(var(--h), var(--s), 60%);
  }
</style>
