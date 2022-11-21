<script>
    export let firstChoice;
    export let secondChoice;
    export let thirdChoice;

    let classSelected = "";
    const classes = [
        "Nauczyciel",
        "1mb",
        "1wb",
        "1at",
        "1ct",
        "1dt",
        "1gt",
        "1it",
        "2mb",
        "2wb",
        "2act",
        "2dgt",
        "2it",
        "2ist",
        "3mb",
        "3wb",
        "3ast",
        "3dgt",
        "3it",
        "4dP",
        "4igP",
        "4iP",
        "4aG",
        "4cgG",
        "4dG",
        "4iG"
    ];

    let name = "";
    let surname = "";
    let email = "";

    function sendForm(e) {
        e.preventDefault();
        const textBody = JSON.stringify({
            first: firstChoice,
            second: secondChoice,
            third: thirdChoice,
            name: name,
            surname: surname,
            class: classSelected,
            email: email
        });
        fetch("/submit_vote", {
            headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
            },
            method: "POST",
            body: textBody
        })
        .then(res => res.text())
        .then(txt => {console.log("GOT:" + txt)});
        console.log(textBody);
    }
</script>

<div class="login">
    <form on:submit={sendForm} class="login--form">
        <input type="text" bind:value={name} placeholder="Imie" class="login--name" required>
        <input type="text" bind:value={surname} placeholder="Nazwisko" class="login--surname" required>
        <!-- <input type="option" placeholder="Klasa" class="login--class"> -->
        <select bind:value={classSelected} required>
            <option value="" disabled selected>Klasa</option>
            {#each classes as c}
                <option value={c}>
                    {c}
                </option>
            {/each}
        </select>
        <input type="email" bind:value={email} placeholder="Email" class="login--mail" required>
        <input type="submit" class="login--submit" required>
    </form>
</div>

<style>
    .login--form {
        padding: 3rem 2rem 2rem;
    }

    .login {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .login--mail {
        padding: .4rem 1rem;
    }
</style>