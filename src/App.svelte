<script>
    /** @type { string } */
    let fName = $state();
</script>

<div>
    <form action="">
        <input
            bind:value={fName}
            type="text"
            name="first-name"
        />
    </form>
</div>
