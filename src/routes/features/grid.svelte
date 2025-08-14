<script>
    const features = [
        {
            title: "Pomodoro Timer",
            description: "Offers a minimalistic pomodoro timer",
            icon: "⏰"
        },
        {
            title: "Leaderboard",
            description: "Coming soon....",
            icon: "🎯"
        },
        {
            title: "Soothing music",
            description: "Featuring multiple soothing background musics to choose from!",
            icon: "📝"
        }
    ];
</script>

<section class="py-10 px-10 bg-blue-300">
    <div class="max-w-6xl mx-auto isolate">
    <h2 class="text-4xl font-semibold text-gray-800 tracking-wide border-b-2 border-gray-500 pb-2 my-6">What We Provide</h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 mt-8">
            {#each features as feature}
                <div class="bg-white p-6 rounded-lg shadow-lg hover:shadow-2xl transition-shadow duration-300 card my-4">
                    <div class="text-4xl mb-4">{feature.icon}</div>
                    <h3 class="text-xl font-semibold mb-2">{feature.title}</h3>
                    <p class="text-gray-600">{feature.description}</p>
                </div>
            {/each}
        </div>
    </div>
</section>


<style>
    .card{
        position: relative;
    }
    .card::after, .card::before{
        content: '';
        position: absolute;
        height: 100%;
        width: 100%;
        background-image: conic-gradient(from var(--angle), #ff4545, #00ff99, #006aff, #ff0095, #ff4545);
        top: 50%;
        left: 50%;
        translate: -50% -50%;
        z-index: -1;
        padding: 15px;
        border-radius: 10px;
        animation: 2s spin linear infinite;
    }
    @property --angle{
        syntax: "<angle>";
        initial-value: 0deg;
        inherits: false;
    }
    .card::before{
        filter: blur(0.4rem);
        opacity: 0.5;
    }
    @keyframes spin{
        from{
            --angle: 0deg;
        }
        to{
            --angle: 360deg;
        }
}
</style>