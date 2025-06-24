<script>
    function goTo(path){
        path = "/home";
        window.location.href = path;
    }
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-blue-400">
    <div class="backdrop-blur-xl bg-white/15 rounded-3xl shadow-2xl border border-white/25 p-8 w-96">
        <form class="space-y-6">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-slate-200 mb-2">Welcome Back</h2>
                <p class="text-slate-200">Sign in to your account</p>
            </div>
            
            <div class="space-y-4">
                <div class="relative">
                    <input type="text" name="email" id="email" placeholder="Email" required class="w-full px-4 py-3 bg-white/80 backdrop-blur-sm border border-white/40 rounded-2xl text-slate-800 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-800 transition-all duration-400">
                </div>
                
                <div class="relative">
                    <input type="password" name="password" id="password" placeholder="Password" required class="w-full px-4 py-3 bg-white/80 backdrop-blur-sm border border-white/40 rounded-2xl text-slate-800 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-800 transition-all duration-400">
                </div>
            </div>
            
            <div class="flex items-end justify-end text-sm">
                <a href="#" class="text-blue-700 hover:text-blue-800 font-medium transition-colors">Forgot password?</a>
            </div>

            <button type="submit" onclick={goTo} class="w-full py-3 px-4 bg-blue-600 hover:bg-blue-700 backdrop-blur-sm border border-blue-500 rounded-2xl text-white font-semibold transition-all duration-300 hover:scale-[1.02] active:scale-[0.98] shadow-lg hover:shadow-xl">Sign In</button>

            <div class="text-center">
                <p class="text-slate-600">Don't have an account? <a href="#" class="text-blue-700 font-semibold hover:text-blue-800 hover:underline transition-colors">Sign up</a></p>
            </div>
        </form>
    </div>
    <div class="absolute bottom-8">Made with ❤️ by Tanish</div>
</div>