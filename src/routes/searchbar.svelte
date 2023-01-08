<script lang="ts">
	import { error } from '@sveltejs/kit';
	import { each } from 'svelte/internal';
	let name = ' ';
	let titles = [];

	async function searchThroughWikiPedia(params: any) {
		const endpoint = `https://en.wikipedia.org/w/api.php?action=query&list=search&prop=info&inprop=url&utf8=&format=json&origin=&srlimit=20&srsearch=${params}&origin=*`;
		const response = await fetch(endpoint);
		if (!response.ok) {
			throw error(1);
		}
		const json = await response.json();
		let result = json.query.search;
		titles = [];
		for (let i = 0; i <= 8; i++) {
			titles.push(result[i].title);
		}
		return result;
	}

	function onInput(param: any) {
		let res = searchThroughWikiPedia(param);
	}
</script>

<main>
	<form action="">
		<input
			class="input"
			placeholder="Search an article..."
			id="input1"
			type="search"
			bind:value={name}
			on:input={(e) => onInput(name)}
		/>
		{#if name.length != 0}
			<div class="searchResults" style="display:block">
				{#each titles as title}
				<br>
					<a href="https://www.example.com">{title}</a>
				{/each}
			</div>
		{/if}
	</form>
</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@700&family=Open+Sans&display=swap');

	.searchResults {
		font-family: 'Open Sans', sans-serif;
		position: absolute;
		background: rgb(255, 255, 255);
		font-size: 17.5px;
		padding-top: 50px;
		padding-left: 25px;
		padding-right: 15px;
		top: -7%;
		box-sizing: border-box;
		border-top-left-radius: 20px;
		border-top-right-radius: 20px;
		border-bottom-left-radius: 20px;
		border-bottom-right-radius: 20px;
		padding-bottom: 15px;
		width: 450px;
		left: -1%;
	}
	a{
		display: block;
		font-size: 18px;
		text-decoration: none;
		font-family: 'Open Sans', sans-serif;
		color: black;
	}
	a:hover{
		color: grey;
	}
	/* position: absolute;
    font-family: 'Open Sans', sans-serif;
    font-size: 17.5px;             
    padding-top: 50px;
    padding-left: 15px;
    padding-right: 15px;
    transform: translate(-50%, 50%);
    background-color: rgb(0, 0, 0);
    box-sizing: border-box;
    border-top-left-radius: 30px;
    border-top-right-radius: 30px;
    border-bottom-left-radius: 20px;
    border-bottom-right-radius: 20px;
    width: 450px;
    display: block;
    user-select: none; */

	input {
		position: absolute;
		top: 0;
		left: 0;
		border: 0;
		width: 100%;
		height: 52px;
		line-height: 75px;
		outline: 0;
		display: block;
		font-size: 16px;
		border-radius: 20px;
		padding: 0 20px;
		z-index: 9;
		box-shadow: 0.5px;
	}
	form {
		position: absolute;
		width: 450px;
		height: 60px;
		left: 50%;
		top: 40%;
		padding: 5px;
		transform: translate(-50%, 50%);
		border-radius: 20px;
		border: 4px solid #f4f3ef;
		box-sizing: border-box;
		background: #f4f3ef;
		transition: 0.04s;
		z-index: 9;
	}
	input::selection {
		text-decoration: line-through;
	}
	/* For Mozilla Firefox */
	input::-moz-selection {
		text-decoration: underline;
	}
	@media only screen and (max-width: 720px) {
        form {
            position: absolute;
            width: 380px;
            height: 60px;
            left: 50%;
            top: 40%;
            padding: 5px;
            transform: translate(-50%, 50%);
            border-radius: 10px;
            border: 4px solid #f4f3ef;
            box-sizing: border-box;
            background: #f4f3ef;
        }
		.searchResults {
			font-family: 'Open Sans', sans-serif;
			position: absolute;
			background: rgb(255, 255, 255);
			font-size: 17.5px;
			padding-top: 50px;
			padding-left: 25px;
			padding-right: 15px;
			top: -7%;
			box-sizing: border-box;
			border-top-left-radius: 20px;
			border-top-right-radius: 20px;
			border-bottom-left-radius: 20px;
			border-bottom-right-radius: 20px;
			padding-bottom: 15px;
			width: 380px;
			left: -1%;
		}
    }    
	.course {
		position: fixed;
		transform: translate(-50%, 50%);
		top: 45%;
		left: 12.5%;
		width: 80%;
		margin: auto;
		text-align: center;
		padding-top: 100px;
	}
	h1 {
		font-size: 36px;
		font-weight: 600;
	}
	p {
		color: #fff;
		font-size: 14px;
		font-weight: 300;
		line-height: 22px;
		padding: 10px;
	}
</style>
