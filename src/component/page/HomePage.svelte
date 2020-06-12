<script>
	import RightCenteredGrid from './../../shared/component/wrapper/RightCenteredGrid.svelte';
	import {fly} from 'svelte/transition';
	import SpinnerElipsis from './../../shared/component/misc/SpinnerElipsis.svelte';
	import InlineCKEditor from './../../shared/component/input/InlineCKEditor.svelte';
	import IconButton from './../../shared/component/button/IconButton.svelte';
	import InputField from './../../shared/component/input/InputField.svelte';
	import CenteredGrid from './../../shared/component/wrapper/CenteredGrid.svelte';
	import Page from './../../shared/component/wrapper/page/Page.svelte';
	import sha256 from './../../shared/script/sha256.js';
	import sortBy from './../../shared/script/sortBy.js';
	let publicKey = "1ac133b7d4cd1708eee4f7d226d483335a7237ee94f910a1ff4a5b4c581d4dfe";
	let promise={
		posts: getPosts(),
		privateKey: getPrivateKey()
	};
	let title;
	let ckeditor;
	let error = "";

	async function getPosts(){
		debugger;
		let response = new Array();
		let list = await fetch("/posts/list.json");
		list = await list.json();
		for(let filename of list){
			try{
				let file = await fetch("/posts/files/"+filename);
				file = await file.json();
				response.push(file);
			}catch(e){
				continue;
			}
		}
		return response;
	}

	async function getPrivateKey(){
		try{
			let response = await fetch("http://127.0.0.1/tncrazvan.github.io-server/get-private-key.php");
			response = await response.text();
			return response;
		}catch(e){
			return false;
		}
	}

	let sending = false;
	async function publish(){
		error = "";
		sending = true;
		let content = ckeditor.getValue();
		if(title.trim() === "" || content.trim() === ""){
			sending = false;
			error = "Title and content of the post cannot be empty.";
			return;
		}
		try{
			let body = JSON.stringify({
				title: title,
				content: content
			});
			let response = await fetch("http://127.0.0.1/tncrazvan.github.io-server/publish-post.php",{
				method: "POST",
				body: body
			});
			response = await response.text();
			sending = false;
			console.log(response);
		}catch(e){
			sending = false;
		}
	}
</script>

<Page>
	<CenteredGrid>
		
			{#await promise.privateKey}
				<div class="display-none"></div>
			{:then key}
				{#if key}
					{#await sha256(key)}
						<div class="display-none"></div>
					{:then hashedKey}
						{#if hashedKey === publicKey}
							<div class="editor" transition:fly={{y:-100,duration: 1000}}>
								<small class="status-online">Server online</small>
								<InputField focus={true} bind:value={title} label="Title"/>
								<div class="editor-content">
									<InlineCKEditor bind:this={ckeditor}>
										Content goes here
									</InlineCKEditor>
								</div>
								<br />
								<RightCenteredGrid>
									{#if sending}
										<SpinnerElipsis />
									{:else}
										{#if error !== ""}
											<small transition:fly={{x:-100,duration:500}} class="error">{error}</small>
											<br />
										{/if}
										<IconButton onClick={publish} icon="send">
											Publish
										</IconButton>
									{/if}
								</RightCenteredGrid>
							</div>
						{/if}
					{/await}
				{/if}
			{/await}

			{#await promise.posts}
				<SpinnerElipsis />
			{:then posts}
				{#each posts.sort(sortBy("lastChange")) as post}
					<div transition:fly={{y:-100,duration: 1000}} class="post">
						<h3>{post.title}</h3>
						<small>{new Date(post.lastChange*1000).toDateString()}</small><br />
						{window.atob(post.content)}
					</div>
				{/each}
			{/await}
		
	</CenteredGrid>
</Page>

<style>
	.error{
		color: #f42934;
	}
	.status-online{
		position: relative;
		color: #aabb26;
	}
	.status-online:after{
		position: absolute;
		right: -1rem;
		top: 0.27rem; 
		content: '';
		width: 7px;
		height: 7px;
		background: #aabb26;
		border-radius: 7px;
	}
	.editor{
		width: 54rem;
		background-color: rgba(0,0,0,0.125);
		padding: 1rem;
		border-radius: 0.3rem;
		border: 1px solid rgba(0,0,0,0.325);
	}

	.editor-content{
		background-color: rgba(0,0,0,0.125);
		padding: 1rem;
		border-radius: 0.3rem;
		border: 1px solid rgba(0,0,0,0.325);
	}

	.post{
		width: 50rem;
		border-bottom: 1px solid var(--main-color);
		padding: 1rem;
	}
</style>