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
}
.dash { 
	color: #3f3f3f;
	margin-left: 16px;
	margin-right: 16px;
}
</style>