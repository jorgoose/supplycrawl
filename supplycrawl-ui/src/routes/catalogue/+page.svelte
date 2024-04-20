<script>
    let searchQuery = '';
    let selectedCategory = 'all';
  
    const categories = [
      'all',
      'Safety & Security',
      'Lighting & Electrical',
      'Tools & Test Instruments',
      'Cleaning & Janitorial',
      'HVAC',
      'Pipes, Hose, Tube & Fittings',
      'Plumbing & Pumps',
      'Metalworking & Fabrication',
      'Motors & Power Transmission',
      'Pneumatics & Hydraulics',
      'Material Handling',
      'Packaging & Shipping',
      'Fasteners, Hardware & Raw Materials',
      'Building & Grounds Maintenance',
      'Tapes, Adhesives & Lubricants',
      'Fleet & Vehicle Maintenance',
      'Lab, Office & Hospitality Supplies',
    ];

    const products = [
      {
        name: "Industrial Drill",
        category: "Tools & Test Instruments",
        description: "High-performance drilling tool suitable for various materials.",
        imageUrl: "https://via.placeholder.com/150x150?text=Drill",
        vendors: [
          { name: "Grainger", price: "$199.99" },
          { name: "McMaster Carr", price: "$189.99" },
          { name: "Fastenal", price: "$205.00" }
        ]
      },
      {
        name: "LED Work Light",
        category: "Lighting & Electrical",
        description: "Durable and bright LED light for workspaces.",
        imageUrl: "https://via.placeholder.com/150x150?text=Light",
        vendors: [
          { name: "Grainger", price: "$59.99" },
          { name: "McMaster Carr", price: "$55.00" },
          { name: "Fastenal", price: "$60.00" }
        ]
      },
      {
        name: "Safety Goggles",
        category: "Safety & Security",
        description: "Protective goggles with anti-fog and scratch resistant lens.",
        imageUrl: "https://via.placeholder.com/150x150?text=Goggles",
        vendors: [
          { name: "Grainger", price: "$15.99" },
          { name: "McMaster Carr", price: "$14.99" },
          { name: "Fastenal", price: "$16.50" }
        ]
      },
      {
        name: "Hydraulic Jack",
        category: "Pneumatics & Hydraulics",
        description: "Heavy-duty jack for lifting and maintenance operations.",
        imageUrl: "https://via.placeholder.com/150x150?text=Jack",
        vendors: [
          { name: "Grainger", price: "$329.99" },
          { name: "McMaster Carr", price: "$340.00" },
          { name: "Fastenal", price: "$350.00" }
        ]
      },
      {
        name: "Pallet Jack",
        category: "Material Handling",
        description: "Robust manual pallet jack, capacity of 5500 lbs.",
        imageUrl: "https://via.placeholder.com/150x150?text=Pallet+Jack",
        vendors: [
          { name: "Grainger", price: "$299.99" },
          { name: "McMaster Carr", price: "$319.99" },
          { name: "Fastenal", price: "$289.99" }
        ]
      },
      {
        name: "Lawn Mower",
        category: "Building & Grounds Maintenance",
        description: "Gas-powered lawn mower with a 52-inch cutting width.",
        imageUrl: "https://via.placeholder.com/150x150?text=Lawn+Mower",
        vendors: [
          { name: "Grainger", price: "$2,499.99" },
          { name: "McMaster Carr", price: "$2,599.99" },
          { name: "Fastenal", price: "$2,450.00" }
        ]
      },
      {
        name: "Office Chair",
        category: "Lab, Office & Hospitality Supplies",
        description: "Ergonomic office chair with lumbar support and adjustable height.",
        imageUrl: "https://via.placeholder.com/150x150?text=Office+Chair",
        vendors: [
          { name: "Grainger", price: "$349.99" },
          { name: "McMaster Carr", price: "$399.99" },
          { name: "Fastenal", price: "$379.99" }
        ]
      }
    ];
</script>
  
  <svelte:head>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css" integrity="sha512-1ycn6IcaQQ40/MKBW2W4Rhis/DbILU74C1vSrLJxCq57o941Ym01SwNsOMqvEBFlcgUa6xLiPY/NS5R+E6ztJQ==" crossorigin="anonymous" referrerpolicy="no-referrer" />
  </svelte:head>
  
  <nav class="bg-zinc-900 py-4 sticky top-0 z-10">
    <div class="container mx-auto px-4 flex items-center justify-between">
      <div class="flex items-center">
        <i class="fas fa-wrench text-orange-400 text-2xl pt-1"></i>
        <h1 class="text-2xl font-bold text-orange-400 ml-2">SupplyCrawl</h1>
      </div>
      <div class="flex items-center">
        <input
          type="text"
          placeholder="Search products..."
          bind:value={searchQuery}
          class="px-3 py-2 bg-zinc-800 border border-zinc-700 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500 text-zinc-400"
        />
      </div>
    </div>
  </nav>
  
  <main class="bg-zinc-900 py-8">
    <div class="container mx-auto px-4">
      <div class="mb-6">
        <h2 class="text-2xl font-bold text-white mb-2">Product Categories</h2>
        <div class="flex flex-wrap -mx-2">
          {#each categories as category}
            <div class="px-2 mb-4">
              <button
                on:click={() => (selectedCategory = category)}
                class={`px-4 py-2 rounded-md ${
                  selectedCategory === category
                    ? 'bg-orange-500 text-white'
                    : 'bg-zinc-800 text-zinc-400 hover:bg-zinc-700'
                } transition duration-300`}
              >
                {category}
              </button>
            </div>
          {/each}
        </div>
      </div>
  
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
        {#each products as product}
          <div class="bg-zinc-800 rounded-lg p-4 flex flex-col items-center text-center shadow-lg transition duration-300 hover:shadow-2xl">
            <img src={product.imageUrl} alt={product.name} class="w-32 h-32 object-cover rounded-md mb-2">
            <h3 class="text-lg font-semibold text-white">{product.name}</h3>
            <p class="text-sm text-zinc-400 mb-3">{product.description}</p>
            <div class="w-full bg-zinc-700 p-2 rounded-md">
              <p class="text-xs text-white">Available from:</p>
              <ul class="text-xs text-zinc-300">
                {#each product.vendors as vendor}
                  <li class="flex justify-between">
                    <span>{vendor.name}</span>
                    <span class="font-bold">{vendor.price}</span>
                  </li>
                {/each}
              </ul>
            </div>
          </div>
        {/each}
      </div>
    </div>
</main>