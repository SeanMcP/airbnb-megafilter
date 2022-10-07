<script lang="ts">
  import data from './data.json'

  let tail

  function handleSubmit(e) {
    e.preventDefault()
    const form = e.target
    let searchParams = new URLSearchParams()
    const checked = form.querySelectorAll('input[type=checkbox]').forEach(n => {
      if (n.checked) {
        searchParams.append('amenities[]', n.dataset.code)
      }
    })
    const string = searchParams.toString()
    if (string) {
      tail = string
    } else {
      alert('Select one or more filters')
    }
  }
</script>

<main>
  <h1>Airbnb MegaFilter</h1>
  <p>Hacked by <a href="https://www.linkedin.com/in/schifeling/">Jeremy Schifeling</a></p>
  <form on:submit={handleSubmit}>
    {#each data as [category, amenities]}
      <fieldset>
        <legend>{category}</legend>
        <section>
          {#each amenities as [label, code]}
            <label>
              <input type="checkbox" data-code={code} />
              <span>{label}</span>
            </label>
          {/each}
        </section>
      </fieldset>
    {/each}
    <footer>
      <button>Generate</button>
      {#if tail}
        <a href={`https://airbnb.com/?${tail}`} target="_blank">Use your Airbnb Megafilter↗</a>
      {/if}
    </footer>
  </form>
  <p>Website made by <a href="https://seanmcp.com">SeanMcP</a></p>
</main>

<style>
  main {
    margin: 1rem auto;
    max-width: 800px;
    padding: 1rem;
  }

  fieldset {
    border: 1px solid #767676;
    border-radius: 2px;
  }

  fieldset + fieldset {
    margin-top: 1rem;
  }

  fieldset section {
    display: grid;
    gap: 0.5rem;
    padding: 0.5rem;
  }

  form footer {
    display: flex;
    gap: 1rem;
    margin-top: 1rem;
  }

  form footer a {
    font-weight: bold;
  }

  @media screen and (min-width: 600px) {
    fieldset section {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  main :is(h1, p) {
    text-align: center;
  }
</style>