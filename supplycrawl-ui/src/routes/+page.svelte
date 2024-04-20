<script lang='ts'>
   import { supabase } from "$lib/supabaseClient";
   import { validateEmail } from "$lib/utils";

   async function handleJoinWaitlist() {
       if (!email) {
           emailError = "Please enter an email address.";
           emailSuccess = "";
           return;
       }

       if (!(await validateEmail(email))) {
           emailError = "Please enter a valid email address.";
           emailSuccess = "";
           return;
       }

       console.log("Email:", email)

       const { data, error } = await supabase.from("waitlist").insert([{ email }]);

       console.log(data, error)

       if (error) {
           if (error.message.includes("duplicate key value violates unique constraint")) {
               emailError = "You're already on the waitlist!";
               emailSuccess = "";
               return;
           }
           emailError = "An unexpected error occurred. Please try again.";
           emailSuccess = "";
           return;
       }

       emailError = "";
       emailSuccess = "You've been added to the waitlist!";
   }

   function scrollToWaitlistForm() {
       const form = document.getElementById('waitlistForm');
       if (form) {
           form.scrollIntoView({ behavior: 'smooth', block: 'center' });
       }
   }

   let email: string = "";
   let emailError: string = "";
   let emailSuccess: string = "";
</script>

<svelte:head>
   <title>SupplyCrawl - Easily Compare Industrial Supply Prices</title>
   <meta name="description" content="Get the best deals on industrial supplies from W.W. Grainger, McMaster Carr, and others. Compare prices, features, and shipping options effortlessly with SupplyCrawl.">
   <meta name="keywords" content="industrial supplies, price comparison, W.W. Grainger, McMaster Carr, screws, bolts, hammers, best deals">
   <meta name="author" content="SupplyCrawl">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <meta property="og:title" content="SupplyCrawl - Easily Compare Industrial Supply Prices">
   <meta property="og:description" content="Get the best deals on industrial supplies from W.W. Grainger, McMaster Carr, and others. Compare prices, features, and shipping options effortlessly with SupplyCrawl.">
   <meta property="og:image" content="https://example.com/supplycrawl-logo.jpg">
   <meta property="og:url" content="https://www.supplycrawl.com">
   <meta name="twitter:card" content="summary_large_image">
   <link rel="canonical" href="https://www.supplycrawl.com">
   <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css" integrity="sha512-1ycn6IcaQQ40/MKBW2W4Rhis/DbILU74C1vSrLJxCq57o941Ym01SwNsOMqvEBFlcgUa6xLiPY/NS5R+E6ztJQ==" crossorigin="anonymous" referrerpolicy="no-referrer" />
</svelte:head>

<nav class="bg-zinc-900 py-4 sticky top-0 z-10">
   <div class="container mx-auto px-4 flex items-center justify-between">
       <div class="flex items-center">
           <i class="fas fa-wrench text-orange-400 text-2xl pt-1"></i>
           <h1 class="text-2xl font-bold text-orange-400 ml-2">SupplyCrawl</h1>
       </div>
   </div>
</nav>
<main>
   <section class="bg-gradient-to-r from-zinc-700 to-zinc-900 py-12 sm:py-24">
       <div class="container mx-auto px-4">
           <div class="max-w-2xl mx-auto text-center mb-8 sm:mb-12">
               <h1 class="text-3xl sm:text-4xl font-bold text-white mb-3 sm:mb-4">Easily Compare Industrial Supply Prices</h1>
               <p class="text-zinc-300 text-base sm:text-lg">Get the best deals from suppliers like W.W. Grainger, McMaster Carr, and others. Compare prices and features effortlessly.</p>
           </div>
           <div class="max-w-md mx-auto" id="waitlistForm">
               <div class="bg-zinc-900 rounded-lg shadow-lg p-4 sm:p-6">
                   <div class="mb-4">
                       <input
                           type="email"
                           bind:value={email}
                           placeholder="Enter your email"
                           class="w-full px-3 py-2 bg-zinc-800 border border-zinc-700 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500 text-zinc-400"
                       />
                   </div>
                   <button
                       on:click={handleJoinWaitlist}
                       class="w-full bg-orange-500 hover:bg-orange-600 text-white font-bold py-2 px-4 rounded-md transition duration-300"
                   >
                       Join Waitlist
                   </button>
                   {#if emailError}
                       <p class="text-red-500 mt-4 text-sm">{emailError}</p>
                   {/if}
                   {#if emailSuccess}
                       <p class="text-green-400 mt-4 text-sm">{emailSuccess}</p>
                   {/if}
               </div>
               <p class="text-zinc-400 mt-4 text-center text-sm">Joining the waitlist will get you free access to the open beta once it launches.</p>
           </div>
       </div>
   </section>
   <section class="bg-zinc-900 py-12 sm:py-24 text-white" style="background-image: url('https://example.com/industrial-background.jpg'); background-size: cover; background-blend-mode: multiply;">
       <div class="container mx-auto px-4">
           <div class="max-w-3xl mx-auto text-center">
               <h2 class="text-4xl sm:text-5xl font-bold text-orange-500 sm:mb-4" style="text-shadow: 2px 2px 8px rgba(0,0,0,0.8);">Save time and money when sourcing industrial supplies</h2>
               <p class="text-xl sm:text-2xl text-zinc-200">Instantly check price, availability, and more across SupplyCrawl's industrial supplies data set.</p>
           </div>
       </div>
   </section>
   <section class="bg-zinc-800 py-12 sm:py-24">
       <div class="container mx-auto px-4">
           <div class="max-w-xl mx-auto text-center mb-8 sm:mb-12">
               <h2 class="text-2xl sm:text-3xl font-bold text-orange-400 mb-3 sm:mb-4">Why Choose SupplyCrawl?</h2>
               <p class="text-zinc-400 text-sm sm:text-base">SupplyCrawl offers unique features to help you save money and make better purchasing decisions.</p>
           </div>
           <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-8">
               <div class="bg-zinc-700 rounded-lg shadow-lg p-6">
                   <div class="flex items-center justify-center mb-4">
                       <i class="fas fa-search-dollar text-orange-400 text-4xl"></i>
                   </div>
                   <h3 class="text-xl font-bold mb-2 text-center text-white">Best Price Finder</h3>
                   <p class="text-zinc-400 text-center">Automatically scan multiple vendors to find the best prices for screws, bolts, hammers, and more.</p>
               </div>
               <div class="bg-zinc-700 rounded-lg shadow-lg p-6">
                   <div class="flex items-center justify-center mb-4">
                       <i class="fas fa-balance-scale text-orange-400 text-4xl"></i>
                   </div>
                   <h3 class="text-xl font-bold mb-2 text-center text-white">Feature Comparison</h3>
                   <p class="text-zinc-400 text-center">Compare product specifications side by side to ensure you get exactly what you need for your project.</p>
               </div>
               <div class="bg-zinc-700 rounded-lg shadow-lg p-6">
                   <div class="flex items-center justify-center mb-4">
                       <i class="fas fa-history text-orange-400 text-4xl"></i>
                   </div>
                   <h3 class="text-xl font-bold mb-2 text-center text-white">Price History</h3>
                   <p class="text-zinc-400 text-center">View the historical price trends of any product to predict future price movements and decide the best time to buy.</p>
               </div>
               <div class="bg-zinc-700 rounded-lg shadow-lg p-6">
                   <div class="flex items-center justify-center mb-4">
                       <i class="fas fa-star text-orange-400 text-4xl"></i>
                   </div>
                   <h3 class="text-xl font-bold mb-2 text-center text-white">Customer Reviews</h3>
                   <p class="text-zinc-400 text-center">Read customer reviews from various vendors to make informed decisions based on others' experiences.</p>
               </div>
               <div class="bg-zinc-700 rounded-lg shadow-lg p-6">
                   <div class="flex items-center justify-center mb-4">
                       <i class="fas fa-shipping-fast text-orange-400 text-4xl"></i>
                   </div>
                   <h3 class="text-xl font-bold mb-2 text-center text-white">Shipping Options</h3>
                   <p class="text-zinc-400 text-center">Get detailed information on shipping options and costs from different suppliers to choose the best delivery method.
               </div>
               <div class="bg-zinc-700 rounded-lg shadow-lg p-6">
                   <div class="flex items-center justify-center mb-4">
                       <i class="fas fa-robot text-orange-400 text-4xl"></i>
                   </div>
                   <h3 class="text-xl font-bold mb-2 text-center text-white">AI-Powered Recommendations</h3>
                   <p class="text-zinc-400 text-center">Receive personalized product suggestions based on your preferred vendors and priorities.</p>
               </div>
           </div>
       </div>
   </section>
</main>

<footer class="bg-zinc-900 py-8">
   <div class="container mx-auto px-4 text-center">
       <p class="text-zinc-400">&copy; 2024 SupplyCrawl. All rights reserved.</p>
   </div>
</footer>
