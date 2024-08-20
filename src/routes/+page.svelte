<script lang="ts">
  import {
    InstantSearch,
    SearchBox,
    Hits,
    Pagination,
    HitsPerPage,
    PoweredBy,
    RefinementList,
    ClearRefinements,
    ToggleRefinement,
    SortBy,
    Highlight,
    HierarchicalMenu,
    Breadcrumb,
    CurrentRefinements,
    Menu,
    RangeInput,
    Stats,
  } from "$lib";

  import { instantMeiliSearch } from '@meilisearch/instant-meilisearch';

  import Panel from "./Panel.svelte";

  const SEARCH_ENDPOINT = import.meta.env.VITE_MEILISEARCH_ENDPOINT;
  const MEILI_MASTER_KEY = import.meta.env.VITE_MEILISEARCH_MASTER_KEY;

  const { searchClient } = instantMeiliSearch(
  'https://ms-adf78ae33284-106.lon.meilisearch.io',
  'a63da4928426f12639e19d62886f621130f3fa9ff3c7534c5d179f0f51c4f303'
);
</script>

<svelte:head>
  <title>svelte-algolia-instantsearch | Demo</title>
</svelte:head>

<InstantSearch indexName="steam-videogames" routing {searchClient}>
  <div class="Container">
    <div>
      <Panel header="Brands"
        ><RefinementList
          attribute="genres"
          searchable
          searchablePlaceholder="Genres"
          showMore
        /></Panel
      >
      <Panel header="Categories">
        <RefinementList
          attribute="categories"
          showMore
        />
      </Panel>
      <Panel header="Platform">
        <RefinementList
          attribute="platforms"
          showMore
        />
      </Panel>
    </div>

    <div class="Search">

      <SearchBox placeholder="Search" />

      <div class="Search-header">
        <PoweredBy />
        <HitsPerPage
          items={[
            { label: "20 hits per page", value: 20, default: true },
            { label: "40 hits per page", value: 40 },
          ]}
        />
        <SortBy
          items={[
            { label: "Name", value: "drills" },
          ]}
        />
      </div>

      <div class="CurrentRefinements">
        <CurrentRefinements
          transformItems={(items) =>
            items.map((item) => {
              const label = item.label.startsWith("hierarchicalCategories")
                ? "Hierarchy"
                : item.label;

              return {
                ...item,
                label,
              };
            })}
        />
        <ClearRefinements translations={{ resetButtonText: "Clear filters" }} />
      </div>

      <Hits let:hit>
        <Highlight attribute="name" classes={{ root: "Hit-label" }} {hit} />
        <span class="Hit-price">${hit.price}</span>
      </Hits>

      <Pagination />
    </div>
  </div>
</InstantSearch>
