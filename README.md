<script>

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  appId: "YOUR_APP_ID"
};

firebase.initializeApp(firebaseConfig);
const auth = firebase.auth();

// REGISTER FUNCTION
function register() {
  const email = document.getElementById("email").value;
  const password = document.getElementById("password").value;

  auth.createUserWithEmailAndPassword(email, password)
    .then((userCredential) => {
      userCredential.user.sendEmailVerification();
      alert("Verification email sent. Please check your email.");
    })
    .catch((error) => {
      alert(error.message);
    });
}

// LOGIN FUNCTION
function login() {
  const email = document.getElementById("email").value;
  const password = document.getElementById("password").value;

  auth.signInWithEmailAndPassword(email, password)
    .then((userCredential) => {
      if (userCredential.user.emailVerified) {
        alert("Login Successful");
      } else {
        alert("Please verify your email first.");
      }
    })
    .catch((error) => {
      alert(error.message);
    });
}

</script>
