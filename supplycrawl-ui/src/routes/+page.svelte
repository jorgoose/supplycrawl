<script lang='ts'>
    // import { supabase } from "$lib/supabaseClient";
    import { validateEmail } from "$lib/utils";

    async function handleJoinWaitlist() {
        if (!email) {
            emailError = "Please enter an email address.";
            emailSuccess = "";
            return;
        }d

        if (!(await validateEmail(email))) {
            emailError = "Please enter a valid email address.";
            emailSuccess = "";
            return;
        }

        console.log("Email:", email)

        // const { data, error } = await supabase.from("waitlist").insert([{ email }]);

        // console.log(data, error)

        // if (error) {
        //     if (error.message.includes("duplicate key value violates unique constraint")) {
        //         emailError = "You're already on the waitlist!";
        //         emailSuccess = "";
        //         return;
        //     }
        //     emailError = "An unexpected error occurred. Please try again.";
        //     emailSuccess = "";
        //     return;
        // }

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
            <div class="max-w-xl mx-auto text-center mb-8 sm:mb-12">
                <h1 class="text-3xl sm:text-4xl font-bold text-white mb-3 sm:mb-4">Compare Industrial Tool Prices Easily</h1>
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
</main>
