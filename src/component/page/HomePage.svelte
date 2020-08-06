<script>
import SectionTitle from './../text/SectionTitle.svelte';
import IconButton from '../button/IconButton.svelte';
import Coding from './../highlighter/Coding.svelte';
import TopMenu from './../menu/TopMenu.svelte';
import { fly, fade } from 'svelte/transition';
import Spinner from '../Spinner.svelte';

let promise = getData();

async function getData(){
	const REGEX = /^\<\?php\r?\n?/g;
	let data = {
		location: "tncrazvan/catpaw-template",
		main: (await (await fetch("/docs/main.php")).text()).replace(REGEX,""),
		event_1: (await (await fetch("/docs/event_1.php")).text()).replace(REGEX,""),
		event_1_2: (await (await fetch("/docs/event_1_2.php")).text()).replace(REGEX,""),
		event_2: (await (await fetch("/docs/event_2.php")).text()).replace(REGEX,""),
		home_page: (await (await fetch("/docs/HomePage.php")).text()).replace(REGEX,""),
		websocket_test: (await (await fetch("/docs/WebSocketTest.php")).text()).replace(REGEX,""),
		websocket_test_constructor_only: (await (await fetch("/docs/WebSocketTest_constructor_only.php")).text()).replace(REGEX,""),
		index: (await (await fetch("/docs/index.php")).text())
	};

	return data;
}
</script>


{#await promise}
<div class="max-full full-height grid-x-center grid-y-center" transition:fade={{duration: 250}}>
	<!-- <SpinnerElipsis /> -->
	<Spinner />
</div>
{:then data}
<div class="row">
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
			Although it's not complete yet, it offers a few useful features such as an MVC-like design pattern and a WebSocket API.
		</p>
		<br/>
		<br/>
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
					Composer is a package manager for php and it also offser an autoloader.<br /><br />
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
		<br />
		<br />
		<br />

		<!--##################### Events #####################-->
		<SectionTitle id="controllers">Events</SectionTitle>
		<p>
			Events will play a central role in your application.<br />
			You can think of events as controllers in a true MVC application, the only difference is 
			that events are not identifies by classes, but instead they are identified by anonymus
			functions.<br />

			Much like a controller, an event has the role of serving/fetching data from/to the incoming requests.<br />
			You can manage both Http and WebSocket requests using events.
		</p>
		<p>
			Basically an event is a function exposed to the ouside world.
		</p>
		<p>
			Your application will have a "<u>main.php</u>" file which will define all your options, including your events and their mapping.<br />

			Here's an example of such a file:<br />
			<Coding padding="1rem" language="php">{data.main}</Coding><br />

			As you can see the script returns an array and as mentioned above, that array contains your application settings, and the fields
			<Coding language="php">$main["events"]["http"]</Coding> and <Coding language="php">$main["events"]["websocket"]</Coding> contain your http and websocket events.<br />

			These events are directly exposed to the web.<br />
		</p>
		<br />
		<br />
		<br />

		<!--##################### HttpEvent /hello/{test} #####################-->
		<SectionTitle id="controllers">HttpEvent /hello/&lbrace;test&rbrace;</SectionTitle>
		The first http path we encounter in the above example is <Coding>/hello/&lbrace;test&rbrace;</Coding>, 
		this path will match any request at <Coding>/test/</Coding> followed by any other string or number.<br />
		
		The assigned function takes in a few parameters, and all of them are completely <b>optional</b>.<br />
		The order of the parameters is not important, your application will automatically inject the parameters accordingly so you don't have to worry about it.<br />
		A quick description on what the parameters we see on this specific function mean:<br />
		<Coding padding="1rem" language="php">{data.event_1}</Coding><br />
		which can also be written as:<br />
		<Coding padding="1rem" language="php">{data.event_1_2}</Coding><br />
		<table>
			<thead>
				<tr>
					<th>Name</th>
					<th>Type</th>
					<th>Description</th>
				</tr>
			</thead>

			<tbody>
				<tr>
					<td><Coding>$test</Coding></td>
					<td><Coding>string</Coding></td>
					<td>
						This parameter is the requested <Coding>&lbrace;test&rbrace;</Coding> path variable<br/><br />
						<b>NOTE:</b>&nbsp;&nbsp;this parameter is a string, however if it were an <Coding>int</Coding> your application would 
						try to convert any given value to int and throw an exception on failure, so be aware of this detail.
					</td>
				</tr>
				<tr>
					<td><Coding>$e</Coding></td>
					<td><Coding>HttpEvent</Coding></td>
					<td>
						This is the HttpEvent that manages the current request.<br />You can also find this object in the global $_EVENT variable.<br />
						This object contains data regarding the current connection, the socket object as a stream and a handful of useful methods to manipulate 
						the request, starting sessions, setting cookies ecc.
					</td>
				</tr>
				<tr>
					<td><Coding>&$onClose</Coding></td>
					<td><Coding>HttpEventOnClose</Coding></td>
					<td>
						This is the pointer to a cycle class. Its <b>run</b> method will be trigered when the connection is over.<br />
						Usually you would want to close your database connection here or do some chores <b>after</b> replying to the user.<br /><br />
						<b>NOTE:</b>&nbsp;&nbsp;it is important that you take in this parameter as a pointer.
					</td>
				</tr>
			</tbody>
		</table>
		<br />
		Usually the function would return a custom object, which would be converted int a json or xml depending on the request "Accept" header, 
		but in this case it return a <Coding>HomePage</Coding> instance, which implement the <Coding>HttpEventInterface</Coding> interface:<br />
		<Coding padding="1rem" language="php">{data.home_page}</Coding>
		<br />
		<br />
		<br />



		<!--##################### HttpEvent /templating/{username} #####################-->
		<SectionTitle id="controllers">HttpEvent /templating/&lbrace;username&rbrace;</SectionTitle>
		The second http path we encounter in the example is <Coding>/templating/&lbrace;username&rbrace;</Coding>, 
		this path will match any request at <Coding>/templating/</Coding> followed by any other string or number.<br />
		
		The same logic as in the previous event applies here, the only difference here is that that, 
		while the previous function returned an <Coding>HomePage</Coding> instance, this time <Coding language="php">ServerFile::include('./templates/index.php',$username);</Coding>
		is returned instead:<br />
		<Coding padding="1rem" language="php">{data.event_2}</Coding><br />
		which in turn returns the buffered contents of the <Coding>./templates/index.php</Coding> file:<br />
		<Coding padding="1rem" language="php">{data.index}</Coding><br />
		<br />
		The returned script makes use of some methods:<br />
		<br />
		<table>
			<thead>
				<tr>
					<th>Name</th>
					<th>Description</th>
				</tr>
			</thead>

			<tbody>
				<tr>
					<td><Coding language="php">Script::args()</Coding></td>
					<td>
						Returns the arguments passed to the 
						<Coding language="php">ServerFile::include('./templates/index.php',...$args)</Coding>
						call.
					</td>
				</tr>
				<tr>
					<td><Coding language="php">&Script::startSession();</Coding></td>
					<td>
						Returns the pointer of the user session array, which you can freely modify.<br />
						If the user does not already have a session or the <b>sessionId</b> cookie is not valid, 
						a new session is created instead and the response <b>sessionId</b> cookie is <u>updated</u>.
					</td>
				</tr>
			</tbody>
		</table>
		<br />
		<br />
		<br />
		
		<!--##################### WebSocketEvent /test #####################-->
		<SectionTitle id="controllers">WebSocketEvent /test</SectionTitle>
		The third and final path we encounter in the example is a websocket path.<br />
		The same exact logic as in the http functions applies here, except this function should not return anything, except for an instance of
		a class that implements <Coding>WebSocketEventInterface</Coding>, in any other cases, 
		the function should simply take in any of the following 3 parameter types as pointers:
		<Coding>WebSocketEventOnOpen</Coding>,<Coding>WebSocketEventOnMessage</Coding>,<Coding>WebSocketEventOnClose</Coding>.<br />
		<br />
		Once the pointers are defined, you can simply overwrite them with your own logic.<br />
		In this case the anonymus function makes an expcetion by returning an instance of a class, specifically the 
		<Coding>WebSocketTest</Coding> class whici implements the <Coding>WebSocketEventInterface</Coding>:<br />
		<Coding padding="1rem" language="php">{data.websocket_test}</Coding><br />
		Once the 3 pointers are defined, you can overwrite them with your own objects, as you can see in the <Coding>WebSocketTest</Coding>
		constructor:
		<Coding padding="1rem" language="php">{data.websocket_test_constructor_only}</Coding>
		<br />
		<br />
		<br />
		<br />
		<!--##################### Injections #####################-->
		<SectionTitle id="controllers">Injections table</SectionTitle>
		Here are all the injections you can make use of.<br />
		Note that your application will inject your parameter based on either its <red>Name</red> or <red>Type</red> or a combination of the two.<br />
		Any other parameter that does not meet any of the requirements in the following table will be injected as <Coding>null</Coding> or as one of 
		<u>path variables</u> based on the variable <red>Name</red>.<br /><br />
		<table>
			<thead>
				<tr>
					<th>Name</th>
					<th>Type</th>
					<th>Description</th>
				</tr>
			</thead>

			<tbody>
				<tr>
					<td><Coding>$e</Coding></td>
					<td><Coding><red>HttpEvent</red></Coding></td>
					<td>
						This is the HttpEvent that manages the current request.<br />You can also find this object in the global $_EVENT variable.<br />
						This object contains data regarding the current connection, the socket object as a stream and a handful of useful methods to manipulate 
						the request, starting sessions, setting cookies ecc.
					</td>
				</tr>
				<tr>
					<td><Coding>&$onClose</Coding></td>
					<td><Coding><red>HttpEventOnClose</red></Coding></td>
					<td>
						This is the pointer to a cycle class. Its <b>run</b> method will be trigered when the connection is over.<br />
						Usually you would want to close your database connection here or do some chores <b>after</b> replying to the user.<br /><br />
						<b>NOTE:</b>&nbsp;&nbsp;it is important that you take in this parameter as a pointer.
					</td>
				</tr>
				<tr>
					<td><Coding><red>&$session</red></Coding></td>
					<td><Coding><red>array</red></Coding></td>
					<td>
						Contains the current use session array, which you can freely modify (is specified as a pointer).<br /><br/>

						This parameter injection requires the variable itself to be named exactly <red>$session</red>.<br />
						Pointer is not required.
					</td>
				</tr>
				<tr>
					<td><Coding><red>$method</red></Coding></td>
					<td><Coding><red>string</red></Coding></td>
					<td>
						Contains the method name of the request.
					</td>
				</tr>
				<tr>
					<td><Coding><red>&$body</red></Coding></td>
					<td><Coding><red>string</red> or <red>int</red> or <red>array</red></Coding></td>
					<td>
						Contains the body of the request.<br /><br />

						This parameter injection requires the variable itself to be named exactly <red>body</red>, of type <red>string</red> or <red>int</red> or <red>array</red>.<br />
						<br />
						Pointer is not required.<br /><br />

						<b>NOTE:</b> if the parameter is specified to be of type <red>array</red>, your application will attempt to parse the body as a json object or array.
					</td>
				</tr>
				<tr>
					<td><Coding>&$onOpen</Coding></td>
					<td><Coding><red>WebSocketEventOnOpen</red></Coding></td>
					<td>
						Pointer to a websocket cycle function.<br />
						This function will trigger when the websocket connection opens (handshake successul).
					</td>
				</tr>
				<tr>
					<td><Coding>&$onMessage</Coding></td>
					<td><Coding><red>WebSocketEventOnMessage</red></Coding></td>
					<td>
						Pointer to a websocket cycle function.<br />
						This function will trigger when the websocket connection recieves a message.
					</td>
				</tr>
				<tr>
					<td><Coding>&$onClose</Coding></td>
					<td><Coding><red><u>WebSocket</u>EventOnClose</red></Coding></td>
					<td>
						Pointer to a websocket cycle function.<br />
						This function will trigger when the websocket connection closes (by either parties).
					</td>
				</tr>
				<tr>
					<td><Coding>&$onClose</Coding></td>
					<td><Coding><red><u>Http</u>EventOnClose</red></Coding></td>
					<td>
						Pointer to an htpp cycle function.<br />
						This function will trigger when the http connection closes (by either parties).
					</td>
				</tr>
				<tr>
					<td><Coding>$cookies</Coding></td>
					<td><Coding><red>HttpRequestCookies</red></Coding></td>
					<td>
						Contains an object that helps you read the cookies sent along with the request.
					</td>
				</tr>
				<tr>
					<td><Coding>$cookies</Coding></td>
					<td><Coding><red>HttpResponseCookies</red></Coding></td>
					<td>
						Contains an object that helps you write the cookies your application will send along with the response.
					</td>
				</tr>
				<tr>
					<td><Coding>$e</Coding></td>
					<td><Coding><red><u>Http</u>Event</red></Coding></td>
					<td>
						Contains an the HttpEvent instance for the current http request.<br /><br />

						<b>NOTE:</b> the HttpEvent class contains a handful of useful methods and allows specific manipulation of the current request and response.
					</td>
				</tr>
				<tr>
					<td><Coding>$e</Coding></td>
					<td><Coding><red><u>WebSocket</u>Event</red></Coding></td>
					<td>
						Contains an the WebSocketEvent instance for the current websocket request.<br /><br />

						<b>NOTE:</b> the WebSocketEvent class contains a handful of useful methods and allows specific manipulation of the current request and response.
					</td>
				</tr>
			</tbody>
		</table>
		<br />
		<br />
		All these injections can be defined in both http events and websocket events.<br />
		This means that it is possible, for example, to manipulate a session from the websocket.
		<br />
		<br />
		<br />
	</div>
</div>
{/await}

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
	red{
		color: red;
	}
</style>
