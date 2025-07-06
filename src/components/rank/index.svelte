<script>
  import Unknown from "./Unknown.svelte";
  import SilverI from "./SilverI.svelte";
  import SilverII from "./SilverII.svelte";
  import SilverIII from "./SilverIII.svelte";
  import SilverIV from "./SilverIV.svelte";
  import SilverElite from "./SilverElite.svelte";
  import SilverEliteMaster from "./SilverEliteMaster.svelte";
  import GoldNovaI from "./GoldNovaI.svelte";
  import GoldNovaII from "./GoldNovaII.svelte";
  import GoldNovaIII from "./GoldNovaIII.svelte";
  import GoldNovaMaster from "./GoldNovaMaster.svelte";
  import MasterGuardianI from "./MasterGuardianI.svelte";
  import MasterGuardianII from "./MasterGuardianII.svelte";
  import MasterGuardianElite from "./MasterGuardianElite.svelte";
  import DistinguishedMasterGuardian from "./DistinguishedMasterGuardian.svelte";
  import LegendaryEagle from "./LegendaryEagle.svelte";
  import LegendaryEagleMaster from "./LegendaryEagleMaster.svelte";
  import SupremeMasterFirstClass from "./SupremeMasterFirstClass.svelte";
  import TheGlobalElite from "./TheGlobalElite.svelte";

  const rank = {
    Unknown,
    SilverI,
    SilverII,
    SilverIII,
    SilverIV,
    SilverElite,
    SilverEliteMaster,
    GoldNovaI,
    GoldNovaII,
    GoldNovaIII,
    GoldNovaMaster,
    MasterGuardianI,
    MasterGuardianII,
    MasterGuardianElite,
    DistinguishedMasterGuardian,
    LegendaryEagle,
    LegendaryEagleMaster,
    SupremeMasterFirstClass,
    TheGlobalElite,
  };

  let { name = "Unknown" } = $props();

  let RankIcon = $derived.by(() => {
    return rank?.[name.replaceAll(" ", "")] ?? unknown;
  });
</script>

<div class="rank">
  <RankIcon />

  <span>{name}</span>
</div>

<style>
  .rank {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    width: auto;
    height: 80px;
    position: relative;
  }

  .rank span {
    position: absolute;
    bottom: -24px;
    color: white;
    font-family: "Rajdhani", sans-serif;
    letter-spacing: 3px;
    text-align: center;
    width: max-content;
    font-size: 0.8rem;
  }

  .rank :global(svg) {
    width: 100%;
    height: 100%;
  }
</style>
