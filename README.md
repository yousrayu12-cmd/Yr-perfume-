// npm install bcrypt
const bcrypt = require('bcrypt');

// Password ko hash karna
async function hashPassword(password) {
  const hash = await bcrypt.hash(password, 10);
  return hash;
}

// Login check karna
async function checkPassword(password, hash) {
  const match = await bcrypt.compare(password, hash);
  return match; // true = sahi password
}let loginAttempts = {};

function canLogin(ip) {
  if (!loginAttempts[ip]) loginAttempts[ip] = 0;
  
  if (loginAttempts[ip] >= 5) {
    console.log("Too many attempts! 15 min wait");
    return false;
  }
  loginAttempts[ip]++;
  return true;
}
