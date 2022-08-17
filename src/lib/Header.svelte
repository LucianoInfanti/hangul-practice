<script>
	export let counter;
	export let tapCount;
</script>

<main>
	<div class="header-wrapper">
		<div class="logo-wrapper">
			<p>한굴 <span class="dash">|</span> practice</p>
		</div>

		<div class="counter-wrapper">
		<p> {counter} <span class="dash">/</span> {tapCount} </p>
		</div>
	</div>
</main>

<style>
.header-wrapper{
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
	margin-top: 16px;
	margin-left: 40px;
	margin-right: 40px;
	transition: 0.4s;
}
.dash { 
	color: #3f3f3f;
	margin-left: 4px;
	transition: 0.4s;
	margin-right: 4px;
}
</style>