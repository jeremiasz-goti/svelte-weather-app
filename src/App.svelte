<script>
  let city = "London";
  let data;
  const fetchWeather = (async () => {
    const response = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=8cbfad668c33b1bdce19655af03e5458&units=metric&lang=pl`
    );
    return await response.json();
  })();

  const handleClick = async () => {
    data = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=8cbfad668c33b1bdce19655af03e5458&units=metric&lang=pl`
    ).then((x) => x.json());
    console.log(data);
  };

  const handleInput = (e) => {
    city = e.target.value;
    console.log(city);
  };

  //   const handleClick = () => {
  //     promise = fetchWeather;
  //     // console.log(fetchWeather);
  //   };
</script>

<main>
  <h1>Svelte weather app</h1>
  <input type="text" on:input={handleInput} />
  <button on:click={handleClick}>check weather</button>
  {#await fetchWeather}
    <p>Checking weather...</p>
  {:then data}
    <h4>Weather in {data["name"]}</h4>
    <img
      src="http://openweathermap.org/img/w/{data['weather'][0]['icon']}.png"
      alt=""
    />
    <p>Temperature {data["main"]["temp"]} C</p>
    <p>{data["weather"][0]["description"]}</p>
  {:catch error}
    <p>An error occurred!</p>
  {/await}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
