<!-- src/routes/+page.svelte -->

<script>
	import Instruction from '../components/Instruction.svelte';
	import Footer from '../components/Footer.svelte';
</script>

<div class="container mx-auto px-4 py-8 flex flex-col md:flex-row">
	<Instruction />

    <section class="md:w-2/3 lg:w-3/4">
        <iframe 
            src="https://www.google.com/maps/d/u/0/embed?mid=1GiVhfp3KgnbYGz1xMNlPGgS4Egyb2hbM" 
            width="100%" 
            height="100%" 
            class="w-full h-screen md:h-[calc(100vh-64px)] rounded-lg shadow-md" 
            allowfullscreen>
        </iframe>
    </section>
</div>
<Footer />
