<script>
	import { Router, Link, Route } from "svelte-navigator";
	import PrivateRoute from "../../PrivateRoute.svelte";
	import Home from "../../pages/home/Home.svelte";
	import Synth from "../../pages/synth/Synth.svelte";
	import Login from "../../pages/login/Login.svelte";



</script>

<Router>
	<nav>
		<Link to="/">Home</Link>
        <Link to="/synth">Synth</Link> 
		<Link to="/login">Login</Link>
		<!-- <Link to="/cart"><img class="cart" src="images/shopping-cart.png" alt="Cart" /></Link> -->
	</nav>
	<div>
		<Route path="/" component={Home}></Route>
        <Route path="/synth" component={Synth}></Route>
		<Route path="/login" component={Login}></Route>
		<PrivateRoute path="/profile" let:location></PrivateRoute> 
	</div>	
</Router>

<style>
	nav {
		position: relative;
		width: 100%;
		background-color: rgb(116, 242, 73);			
	}

	/*img {
	
  left: 10%;
  top: 10%;
  width: 10%;
  height: auto;
}

img:hover {
  box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
}
	*/
</style>