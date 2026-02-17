<!DOCTYPE html>
<html>
<head>
  <title>Jan Nivesh Login</title>

  <script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-auth-compat.js"></script>
</head>

<body>

<h2>Jan Nivesh Phone Login</h2>

<input type="text" id="phone" placeholder="+91XXXXXXXXXX">
<button onclick="sendOTP()">Send OTP</button>

<br><br>

<input type="text" id="otp" placeholder="Enter OTP">
<button onclick="verifyOTP()">Verify OTP</button>

<div id="recaptcha-container"></div>

<script>

const firebaseConfig = {
  apiKey: "AIzaSyDP6deMg1DmjeUpejx7a_6kBEN6m_Q8iA8",
  authDomain: "jannivesh-a55cb.firebaseapp.com",
  projectId: "jannivesh-a55cb",
  storageBucket: "jannivesh-a55cb.firebasestorage.app",
  messagingSenderId: "853197155676",
  appId: "1:853197155676:web:b77625a46627b0cf66e599",
  measurementId: "G-J2FXXR33X5"
};

firebase.initializeApp(firebaseConfig);
const auth = firebase.auth();

window.recaptchaVerifier = new firebase.auth.RecaptchaVerifier(
  'recaptcha-container',
  { size: 'invisible' }
);

function sendOTP() {
  const phone = document.getElementById('phone').value;

  auth.signInWithPhoneNumber(phone, window.recaptchaVerifier)
    .then(function (confirmationResult) {
      window.confirmationResult = confirmationResult;
      alert("OTP Sent");
    })
    .catch(function(error){
      alert(error.message);
    });
}

function verifyOTP() {
  const otp = document.getElementById('otp').value;

  window.confirmationResult.confirm(otp)
    .then(function () {
      alert("Login Successful");
    })
    .catch(function(error){
      alert("Invalid OTP");
    });
}

</script>

</body>
</html>
