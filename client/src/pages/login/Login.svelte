<script>
  import { useNavigate, useLocation } from "svelte-navigator";
import { loggedInUser } from "../../../../../synthesizer-webshop/client/src/store/store.js";
  import { signupURL, fetchUser, makeOptions } from "../../store/globalStore.js";
  //import { toast } from "@zerodevx/svelte-toast";
  
  const navigate = useNavigate();
  const location = useLocation();
  
  let userData = {};
  
  let newUser = {};
  
  function handleSubmit() {
    const fetchedUserData = fetchUser(userData);
    $loggedInUser = fetchedUserData;
    console.log(fetchedUserData);
    const from = ($location.state && $location.state.from) || "/";
        navigate("/profile", from, { replace: true });
    
  }

  async function handleLogout() {
    const options = makeOptions("POST", userData);
    await fetch("http://localhost:3000/api/users/logout", options);
        const from = ($location.state && $location.state.from) || "/";
        navigate("/", from, { replace: true });  
    }
     
  async function signup() {
    const res = await fetch(signupURL, {
      headers: {
        "content-type": "application/json",
      },
      method: "POST",
      body: JSON.stringify(newUser),
    });
    
    //toastr.success('Have fun storming the castle!', 'Miracle Max Says')
  };
</script>

<div class="login">
<h1>Login</h1>
<label for="email">Email</label>
<input placeholder="Email" name="email"  bind:value={userData.email}>

<label for="password">Password</label>
<input type="password" placeholder="password" name="password" bind:value={userData.password}>
<button type="submit" on:click={handleSubmit}>Login</button>
</div>

<h3> or </h3>
<div class="signup">
<h1>Signup</h1>
<label for="email">Email</label>
<input placeholder="Email" name="email" bind:value={newUser.email}>
    
<label for="password">Password</label>
<input type="password" placeholder="password" name="password" bind:value={newUser.password}>
<button type="submit" on:click={signup}>Sign Up</button>
</div>


   