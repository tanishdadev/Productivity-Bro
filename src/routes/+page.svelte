<script>
	import { onMount } from 'svelte';

	const firebaseConfig = {
	    apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
	    authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
	    projectId: import.meta.env.VITE_FIREBASE_PROJECT_ID,
	    storageBucket: import.meta.env.VITE_FIREBASE_STORAGE_BUCKET,
	    messagingSenderId: import.meta.env.VITE_FIREBASE_MESSAGING_SENDER_ID,
	    appId: import.meta.env.VITE_FIREBASE_APP_ID
	};

	function showMessage(message, divID) {
		const messagediv = document.getElementById(divID);
		messagediv.style.display = "block";
		messagediv.innerHTML = message;
		messagediv.style.opacity = 1;
		setTimeout(() => {
            messagediv.style.display = "none";
			messagediv.style.opacity = 0;
		}, 5000);
	}

	onMount(async () => {
		const { initializeApp } = await import("https://www.gstatic.com/firebasejs/11.9.1/firebase-app.js");
		const { getAuth, signInWithEmailAndPassword } = await import("https://www.gstatic.com/firebasejs/11.9.1/firebase-auth.js");

		const app = initializeApp(firebaseConfig);
		const auth = getAuth(app);

		const signIn = document.getElementById('submitsignIn');

		signIn?.addEventListener('click', (event) => {
			event.preventDefault();
			const email = document.getElementById('email').value;
			const password = document.getElementById('password').value;

			signInWithEmailAndPassword(auth, email, password)
				.then((userCredentials) => {
					showMessage('Sign In is successful!', 'signInMessage');
					localStorage.setItem('signedInUserId', userCredentials.user.uid);
					location.replace('/home');
				})
				.catch((error) => {
					const errorCode = error.code;
					if (errorCode === 'auth/invalid-credential') {
						showMessage('Invalid email or password!', 'signInMessage');
					} 
                    else {
						showMessage('User does not exist!', 'signInMessage');
					}
				});
		});
	});
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-blue-400">
    <div class="backdrop-blur-xl bg-white/15 rounded-3xl shadow-2xl border border-white/25 p-8 w-96">
        <form class="space-y-6">
            <div class="text-center">
                <h2 class="text-3xl font-bold text-slate-200 mb-2">Welcome Back</h2>
                <p class="text-slate-200">Sign in to your account</p>
            </div>

            <div id="signInMessage" class="hidden text-white bg-amber-500 [padding:10px_20px] m2 rounded-md text-base"></div>
            
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

            <button type="submit" id="submitsignIn" class="w-full py-3 px-4 bg-blue-600 hover:bg-blue-700 hover:cursor-pointer backdrop-blur-sm border border-blue-500 rounded-2xl text-white font-semibold transition-all duration-300 hover:scale-[1.02] active:scale-[0.98] shadow-lg hover:shadow-xl">Sign In</button>

            <div class="text-center">
                <p class="text-slate-600">Don't have an account? <a href="/signup" class="text-blue-700 font-semibold hover:text-blue-800 hover:underline transition-colors">Sign up</a></p>
            </div>
        </form>
    </div>
    <div class="absolute bottom-8">Made with ❤️ by Tanish</div>
</div>