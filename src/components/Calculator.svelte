<script>
  import Rank from "./rank/index.svelte";
  import Rating from "./Rating.svelte";

  const rankRange = [
    {
      start: 0,
      end: 3754,
      rank: "Silver I",
    },
    {
      start: 3755,
      end: 4997,
      rank: "Silver II",
    },
    {
      start: 4998,
      end: 5723,
      rank: "Silver III",
    },
    {
      start: 5724,
      end: 6855,
      rank: "Silver IV",
    },
    {
      start: 6856,
      end: 7950,
      rank: "Silver Elite",
    },
    {
      start: 7951,
      end: 9026,
      rank: "Silver Elite Master",
    },
    {
      start: 9027,
      end: 9999,
      rank: "Gold Nova I",
    },
    {
      start: 10000,
      end: 11036,
      rank: "Gold Nova II",
    },
    {
      start: 11037,
      end: 12136,
      rank: "Gold Nova III",
    },
    {
      start: 12137,
      end: 13206,
      rank: "Gold Nova Master",
    },
    {
      start: 13207,
      end: 14304,
      rank: "Master Guardian I",
    },
    {
      start: 14305,
      end: 15114,
      rank: "Master Guardian II",
    },
    {
      start: 15115,
      end: 16326,
      rank: "Master Guardian Elite",
    },
    {
      start: 16327,
      end: 17259,
      rank: "Distinguished Master Guardian",
    },
    {
      start: 17260,
      end: 18265,
      rank: "Legendary Eagle",
    },
    {
      start: 18266,
      end: 19879,
      rank: "Legendary Eagle Master",
    },
    {
      start: 19880,
      end: 21847,
      rank: "Supreme Master First Class",
    },
    {
      start: 21848,
      end: 99999,
      rank: "The Global Elite",
    },
  ];

  let cs2Rating = $state(3500);

  const clampedCs2Rating = $derived(Math.min(Math.max(cs2Rating, 0), 99999));

  const rankName = $derived.by(() => {
    for (const range of rankRange) {
      if (clampedCs2Rating >= range.start && clampedCs2Rating <= range.end) {
        return range.rank;
      }
    }

    return "Unknown";
  });
</script>

<div class="calculator">
  <input
    class="calculator__input"
    type="number"
    bind:value={cs2Rating}
    onkeypress={(event) => {
      if (
        isNaN(parseInt(event.key, 10)) &&
        !["Backspace"].includes(event.key)
      ) {
        event.preventDefault();
      }
    }}
    placeholder="Enter CS2 Rating"
  />

  <div class="calculator__result" aria-hidden="true">
    <Rating rating={clampedCs2Rating} />

    <svg
      class="calculator__arrow"
      xmlns="http://www.w3.org/2000/svg"
      width="32"
      height="32"
      viewBox="0 0 24 24"
      fill="none"
      stroke="white"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
      aria-hidden="true"
      ><path d="M18 8L22 12L18 16" /><path d="M2 12H22" /></svg
    >

    <Rank name={rankName} />
  </div>

  <p class="screen-reader-only" aria-live="polite">
    A CS2 Rating of {clampedCs2Rating} is equal to {rankName}.
  </p>
</div>

<style>
  .calculator {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 48px;
  }

  .calculator__input {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border-radius: 4px;
    box-sizing: border-box;
  }

  .calculator__result {
    display: flex;
    flex: 1;
    align-items: center;
    justify-content: center;
    gap: 48px;
  }

  .screen-reader-only {
    clip: rect(0 0 0 0);
    clip-path: inset(50%);
    height: 1px;
    overflow: hidden;
    position: absolute;
    white-space: nowrap;
    width: 1px;
  }

  @media (max-width: 800px) {
    .calculator__result {
      flex-direction: column;
      gap: 18px;
    }

    .calculator__arrow {
      transform: rotate(90deg);
    }
  }
</style>
