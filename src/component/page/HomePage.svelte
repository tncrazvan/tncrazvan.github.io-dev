<script>
	import SectionTitle from './../text/SectionTitle.svelte';
	import IconButton from './../../shared/component/button/IconButton.svelte';
	import Coding from './../highlighter/Coding.svelte';
	import SpinnerElipsis from './../../shared/component/misc/SpinnerElipsis.svelte';
	import TopMenu from './../menu/TopMenu.svelte';
	import { fly, fade } from 'svelte/transition';
	import CenteredGrid from './../../shared/component/wrapper/CenteredGrid.svelte';
	import Page from './../../shared/component/wrapper/page/Page.svelte';

	let promise = getData();
	async function getData(){
		const REGEX = /^\<\?php\r?\n?/g;
		let data = {
			location: "tncrazvan/catpawskeleton",
			http: (await (await fetch("/docs/examples/config.php")).text()).replace(REGEX,""),
			example: {
				controller1: (await (await fetch("/docs/examples/Hello/1.php")).text()).replace(REGEX,""),
				controller3: (await (await fetch("/docs/examples/Hello/3.php")).text()).replace(REGEX,""),
				controller4: (await (await fetch("/docs/examples/Hello/4.php")).text()).replace(REGEX,""),
				controller5: (await (await fetch("/docs/examples/Hello/5.php")).text()).replace(REGEX,""),
			}
		};

		return data;
	}
</script>

<Page desktopWidth="100%">
	{#await promise}
		<div transition:fade={{duration: 250}}>
			<SpinnerElipsis />
		</div>
	{:then data}
	<div class="
		col
		offset-s0 s12
		offset-m0 m12
		offset-l1 l10
		offset-xl2 xl8
	">
		<TopMenu />

		<img class="top-logo" src="/images/logo.png" alt="logo">
		<h4 class="top-title">What is CatPaw?</h4>
		<p>
			CatPaw is a lightweight web server written in Php for <b>Linux</b>.<br>
			Although it's not complete yet, it offers a few useful features such as an MVC design pattern and a WebSocket API.
		</p>
		<br/>

		<!--##################### HOW TO START #####################-->
		<SectionTitle id="start">How to start</SectionTitle>
		<ul class="collection">
			<li class="collection-item">
					<b>Make sure you have php 7.2 or higher installed</b>
			</li>
			<li class="collection-item">
					<b>Install composer</b><br />
					In order to run the server you'll need composer.<br />
					Composer is a package manager for php and it also offser an autoloader.
					<hr>
					<a target="_blank" href="https://getcomposer.org/">
						<IconButton>Download composer</IconButton>
					</a>
			</li>
			<li class="collection-item">
					<b>Make a project</b><br />
					Run 
					<Coding language="bash">composer create-project <b>{data.location}</b> ProjectName -sdev</Coding>
					to make a new CatPaw project from the public skeleton template
			</li>
			<li class="collection-item">
					<b>Update the project</b><br />
					Now you need to get all the required libraries for the website to work, so run 
					<Coding language="bash">composer update</Coding>
					inside the project directory
			</li>
			<li class="collection-item">
					<b>Run the server</b><br  />
					Now you need to run CatPaw from the terminal using 
					<Coding language="bash">sudo ./start</Coding>
			</li>
		</ul>


		<!--##################### CONTROLLERS #####################-->
		<SectionTitle id="controllers">Controllers</SectionTitle>
		<p>
			Controllers play a central role when developing a web service.<br />
			A controller has the role of serving or fetching data from client http or websocket requests.
		</p>
		<p>
			Controller don't have a specific file system location, infact, any class that extends the abstract class 
			<coding language="php">\com\github\tncrazvan\catpaw\http\HttpController</coding> is an http controller.
			On the other hand, any class extending <Coding language="php">\com\github\tncrazvan\catpaw\websocket\WebSocketController</Coding>
			is a websocket controller.<br />
		</p>
		<p>
			These controllers however are not exposed to the web, which means they are not attatched to any specific route yet.<br />
			In order to expose a controller you must define it's classname in <b>config/config.php</b> in the <Coding language="js">controllers.http</Coding> field.
		</p>
		<p>
			Open <b>/config/config.php</b> in a text editor. You should see something like this:<br /><br />
			<Coding language="json">{data.http}</Coding><br /><br />
			All you need to do in order to define a namespace for your controller is to add your class to the  
			<Coding language="json">controllers.http</Coding> field.<br />
			You must do the same for websocket controllers, except you must act on the <Coding language="json">controllers.websocket</Coding>
			field.
		</p>
		<p>
			The CatPaw library defines some virtual paths for your by default, such as "@file" which ensures that the server can serve normal files and "@404" which ensures the server responds with a 404 Not Found when the requested resource cannot be found, instead of hanging the socket connection.<br />
			An ascii table is printed to the console when running the server, this table contains all the information your server uses, including all these virtual paths and your custom paths
		</p>


		<!--##################### CONTROLLER EXAMPLE #####################-->
		<SectionTitle id="controllers">Controller Example</SectionTitle>
		<ul class="collection">
			<li class="collection-item">
					<p>
						We're gonna use the default namespace for this example.<br />
						Make a new file under <b>/controllers/http/</b> named <b>Hello.php</b> 
						and throw in the basics: namespace and a class with the same name as the file:
					</p>
					<Coding language="php">{data.example.controller1}</Coding>
			</li>
			<li class="collection-item">
					<p>
						Now we extend the HttpController in order to allow this class to act as a controller.
					</p>
					<Coding language="php">{data.example.controller3}</Coding>
			</li>
			<li class="collection-item">
					<p>
						The <b>main</b> method is called only when no method is specified in the controller request, 
						so we can look at it as a fallback method.<br />
						The <b>onClose</b> method is always called if defined in your class.<br />
						This method is supposed to be used to undo changes, 
						or close database connections before closing the http connection itself.<br />
						It's a cleanup method.
					</p>
					<br />
					<p>
						The next step is to reply to the client with a message.<br />
						We'll reply with "hello".
					</p>
					<p>
						One way to reply to the client is to simply call the method
						<b>HttpEvent::send($data)</b>.<br />
						Note that HttpController extends HttpEvent, thus your controller inherits HttpEvent::send.<br />
						Here's an example:
					</p>
					<Coding language="php">{data.example.controller4}</Coding>
					<p>
						Another way of replying is to return a proper HttpResponse object.
					</p>
					<Coding language="php">{data.example.controller5}</Coding>
			</li>
		</ul>


	</div>
	{/await}
</Page>

<style>
	.top-logo{
		position: relative;
		top: 1em;
		width: 5em;
		display: inline-block;
		border: 1px solid #f1f1f1;
		border-radius: 50%;
	}
	.top-title{
		margin-left: 1em;
		display: inline-block;
	}
</style>