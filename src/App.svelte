<script lang="ts">
import Note from "./components/Note.svelte";

type NoteType = {
	title: string;
	body: string;
};

let notes: Array<NoteType> = [];

const data = localStorage.getItem("notes");
if (data) notes = JSON.parse(data);

let title: string = "";
let body: string = "";

function onSubmit() {
	let note: NoteType = {
		title: title,
		body: body
	};
	notes.push(note);
	localStorage.setItem("notes", JSON.stringify(notes));
}
</script>

<div class="container">
	<header>
		<h1>Notes App</h1>
	</header>
	<main>
		{#each notes as note}
			<Note title={note.title} body={note.body} />
		{/each}
		<div class="note">
			<form on:submit={onSubmit}>
				<input type="text" placeholder="Note Title" bind:value={title} />
				<textarea placeholder="Note Body" bind:value={body}></textarea>
				<input type="submit" value="Add Note" />
			</form>
		</div>
	</main>
</div>

<style>
body {
  height: 100%;
  width: 100%;
  margin: 0;
}

.container {
  width: 100%;
  height: auto;
  margin: 0;
  display: flex;
  flex-direction: column;
}
.container header {
  display: flex;
  align-items: center;
  width: 100%;
  height: 56px;
  background-color: #4e78b8;
  color: white;
}
.container header h1 {
  margin-left: 6px;
}
.container main {
  margin: 10px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  grid-gap: 1rem;
  align-items: center;
}
.container main .note {
  display: flex;
  flex-direction: column;
  padding: 10px;
  background-color: #a15fbb;
  border-radius: 5px;
}
.container main .note form {
  display: flex;
  flex-direction: column;
}
.container main .note form textarea {
  resize: none;
}
</style>