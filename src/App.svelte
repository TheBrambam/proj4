<script>
  let switched = false;

  // Default order
  const buttons = [
    'Check-in',
    'Call Trans',
    '3',
    'Waiting',
    'Head/Latrine',
    '6',
    'Schedule',
    'Benefits',
    '9',
    '*',
    'Nurse',
    '#'
  ];

  // Remapping when switch is ON
  const map = {
    'Check-in': '1',
    'Call Trans': 'Check-In',
    '3': 'Call Trans',
    'Waiting': '4',
    'Head/Latrine': 'Waiting',
    '6': 'Head/Latrine',
    'Schedule': '7',
    'Benefits': 'Schedule',
    '9': 'Benefits'
  };

  function transformedButtons() {
    if (!switched) return buttons;

    // Apply mapping for hand change
    return buttons.map(b => map[b] ?? b);
  }

function handleClick(label) {
  // Page routes
  const routes = {
    "Benefits": "benefits.html",
    "Waiting": "waiting.html"
  };

  if (routes[label]) {
    window.location.href = routes[label];
    return;
  }

  console.log("Clicked:", label);
}
</script>

<main class="app">
  <div class="header">
    <h1>VA Quick App</h1>

    <!-- Switch -->
    <label class="switch">
      <input type="checkbox" bind:checked={switched} />
      <span class="slider"></span>
    </label>
  </div>

  <div class="button-grid">
    {#each transformedButtons() as label}
      <button class="rounded-button" on:click={() => handleClick(label)}>
        {label}
      </button>
    {/each}
  </div>
</main>

<style>
  .app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    font-family: system-ui, sans-serif;
    background: #030303;
    padding: 1.5rem;
  }

  .header {
    width: 100%;
    max-width: 400px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    margin-bottom: 1.25rem;
  }

  h1 {
    font-size: 1.4rem;
  }

  /* Switch styling */
  .switch {
    position: relative;
    width: 52px;
    height: 28px;
  }
  .switch input {
    opacity: 0;
    width: 0;
    height: 0;
  }
  .slider {
    position: absolute;
    inset: 0;
    cursor: pointer;
    background: #555;
    border-radius: 34px;
    transition: 0.3s;
  }
  .slider:before {
    content: "";
    position: absolute;
    width: 22px;
    height: 22px;
    left: 3px;
    bottom: 3px;
    background: white;
    border-radius: 50%;
    transition: 0.3s;
  }
  input:checked + .slider {
    background: #2563eb;
  }
  input:checked + .slider:before {
    transform: translateX(24px);
  }

  .button-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
    width: 100%;
    max-width: 400px;
  }

  .rounded-button {
    border: none;
    border-radius: 9999px;
    padding: 0.9rem 1.2rem;
    background: #2563eb;
    color: white;
    font-size: 1rem;
    cursor: pointer;
    transition: 0.15s;
  }

  .rounded-button:hover {
    background: #1d4ed8;
  }

  .rounded-button:active {
    background: #1e40af;
  }
</style>
