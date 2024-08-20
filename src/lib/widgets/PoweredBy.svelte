<script lang="ts">
  import { connectPoweredBy } from "instantsearch.js/es/connectors";
  import type { PoweredByConnectorParams } from "instantsearch.js/es/connectors/powered-by/connectPoweredBy";

  import connect from "$lib/connect";
  import { cx } from "$lib/utils";

  type PoweredByClassNames = {
    /**
     * Class names to apply to the root element
     */
    root: string;
    /**
     * Class names to apply to the root element with the light theme
     */
    light: string;
    /**
     * Class names to apply to the root element with the dark theme
     */
    dark: string;
    /**
     * Class names to apply to the link element
     */
    link: string;
    /**
     * Class names to apply to the SVG logo
     */
    logo: string;
  };

  type $$Props = PoweredByConnectorParams & {
    classes?: Partial<PoweredByClassNames>;
    theme?: "light" | "dark";
  };
  export let url: $$Props["url"] = undefined;
  export let theme: $$Props["theme"] = "light";
  export let classes: NonNullable<$$Props["classes"]> = {};

  const state = connect(connectPoweredBy, { url }, { $$widgetType: "svelte-ais.PoweredBy" });
  $: ({ url: stateUrl } = $state);
</script>

<div
  class={cx(
    "ais-PoweredBy",
    classes.root,
    theme === "dark" && cx("ais-PoweredBy--dark", classes.dark),
    theme === "light" && cx("ais-PoweredBy--light", classes.light),
  )}
><span>Powered by&nbsp;</span>
  <a
    href="https://www.meilisearch.com"
    target="_blank"
    class={cx("ais-PoweredBy-link", classes.link)}
    aria-label="Search by Meilsearch"
    rel="noopener noreferrer"
  >
 <svg xmlns="http://www.w3.org/2000/svg" width="1.71em" height="1em" viewBox="0 0 256 150"><defs><linearGradient id="logosMeilisearch0" x1="153.821%" x2="19.172%" y1="-7.638%" y2="89.239%"><stop offset="0%" stop-color="#ff5caa"/><stop offset="100%" stop-color="#ff4e62"/></linearGradient><linearGradient id="logosMeilisearch1" x1="117.325%" x2="-17.323%" y1="-7.638%" y2="89.238%"><stop offset="0%" stop-color="#ff5caa"/><stop offset="100%" stop-color="#ff4e62"/></linearGradient><linearGradient id="logosMeilisearch2" x1="80.828%" x2="-53.821%" y1="-7.638%" y2="89.238%"><stop offset="0%" stop-color="#ff5caa"/><stop offset="100%" stop-color="#ff4e62"/></linearGradient></defs><path fill="url(#logosMeilisearch0)" d="M0 149.288L47.297 28.277A44.46 44.46 0 0 1 88.708 0h28.515L69.926 121.012a44.46 44.46 0 0 1-41.411 28.276z"/><path fill="url(#logosMeilisearch1)" d="m69.386 149.289l47.297-121.012A44.46 44.46 0 0 1 158.095 0h28.514l-47.297 121.012a44.46 44.46 0 0 1-41.411 28.277z"/><path fill="url(#logosMeilisearch2)" d="m138.777 149.289l47.297-121.012A44.46 44.46 0 0 1 227.484 0H256l-47.297 121.012a44.46 44.46 0 0 1-41.412 28.277z"/></svg>
  </a>
</div>
