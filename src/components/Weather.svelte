<script lang="ts">
  const API_KEY = "72eed4b5787d977eb1ac6d374b0ae807";
  let city = "Caracas, Distrito Capital";
  const getWeatherData = async () => {
    const res = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&lang=es&appid=${API_KEY}`
    );

    const data = await res.json();
    return data;
  };

  let promise = getWeatherData();
</script>

<div class="container">
  <div class="row">
    <div class="col-12">
      <form action="">
        <label for="">
          City: <input type="text" class="form-control" />
        </label>
      </form>
    </div>
  </div>
  <div class="row mt-5">
    {#await promise}
      loading...
    {:then weather}
      <div class="col-12 col-md-6">
        <h1>
          <img
            class="bg-secondary"
            src={`https://openweathermap.org/img/wn/${weather.weather[0].icon}.png`}
            alt=""
          />
          {weather.main.temp} °C
        </h1>
        <h4>
          City: <span class="fw-bold"
            >{weather.name}, {weather.sys.country}</span
          >
        </h4>
        <h4>
          Weather: <span class="fw-bold">{weather.weather[0].description}</span>
        </h4>
      </div>
      <div class="col-12 col-md-6">
        <h4>
          Máxima temperatura: <span class="fw-bold text-danger"
            >{weather.main.temp_max} °C</span
          >
        </h4>
        <h4>
          Mínima temperatura: <span class="fw-bold text-primary"
            >{weather.main.temp_min} °C</span
          >
        </h4>
      </div>
    {/await}
  </div>
</div>
