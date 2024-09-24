<script>
    import Chronik_1 from "./headings/1_Chronik.json";
    import Johannes_1 from "./headings/1_Johannes.json";
    import Könige_1 from "./headings/1_Könige.json";
    import Korinther_1 from "./headings/1_Korinther.json";
    import Mose_1 from "./headings/1_Mose.json";
    import Petrus_1 from "./headings/1_Petrus.json";
    import Samuel_1 from "./headings/1_Samuel.json";
    import Thessalonicher_1 from "./headings/1_Thessalonicher.json";
    import Timotheus_1 from "./headings/1_Timotheus.json";
    import Chronik_2 from "./headings/2_Chronik.json";
    import Johannes_2 from "./headings/2_Johannes.json";
    import Könige_2 from "./headings/2_Könige.json";
    import Korinther_2 from "./headings/2_Korinther.json";
    import Mose_2 from "./headings/2_Mose.json";
    import Petrus_2 from "./headings/2_Petrus.json";
    import Samuel_2 from "./headings/2_Samuel.json";
    import Thessalonicher_2 from "./headings/2_Thessalonicher.json";
    import Timotheus_2 from "./headings/2_Timotheus.json";
    import Johannes_3 from "./headings/3_Johannes.json";
    import Mose_3 from "./headings/3_Mose.json";
    import Mose_4 from "./headings/4_Mose.json";
    import Mose_5 from "./headings/5_Mose.json";
    import Amos from "./headings/Amos.json";
    import Apostelgeschichte from "./headings/Apostelgeschichte.json";
    import Daniel from "./headings/Daniel.json";
    import Epheser from "./headings/Epheser.json";
    import Esra from "./headings/Esra.json";
    import Esther from "./headings/Esther.json";
    import Galater from "./headings/Galater.json";
    import Habakuk from "./headings/Habakuk.json";
    import Haggai from "./headings/Haggai.json";
    import Hebräer from "./headings/Hebräer.json";
    import Hesekiel from "./headings/Hesekiel.json";
    import Hiob from "./headings/Hiob.json";
    import Hohelied from "./headings/Hohelied.json";
    import Hosea from "./headings/Hosea.json";
    import Jakobus from "./headings/Jakobus.json";
    import Jeremia from "./headings/Jeremia.json";
    import Jesaja from "./headings/Jesaja.json";
    import Joel from "./headings/Joel.json";
    import Johannes from "./headings/Johannes.json";
    import Jona from "./headings/Jona.json";
    import Josua from "./headings/Josua.json";
    import Judas from "./headings/Judas.json";
    import Klagelieder from "./headings/Klagelieder.json";
    import Kolosser from "./headings/Kolosser.json";
    import Lukas from "./headings/Lukas.json";
    import Maleachi from "./headings/Maleachi.json";
    import Markus from "./headings/Markus.json";
    import Matthäus from "./headings/Matthäus.json";
    import Micha from "./headings/Micha.json";
    import Nahum from "./headings/Nahum.json";
    import Nehemia from "./headings/Nehemia.json";
    import Obadja from "./headings/Obadja.json";
    import Offenbarung from "./headings/Offenbarung.json";
    import Philemon from "./headings/Philemon.json";
    import Philipper from "./headings/Philipper.json";
    import Prediger from "./headings/Prediger.json";
    import Psalmen from "./headings/Psalmen.json";
    import Richter from "./headings/Richter.json";
    import Römer from "./headings/Römer.json";
    import Ruth from "./headings/Ruth.json";
    import Sacharja from "./headings/Sacharja.json";
    import Sprüche from "./headings/Sprüche.json";
    import Titus from "./headings/Titus.json";
    import Zephanja from "./headings/Zephanja.json";

    let books = [
        [Mose_1, Mose_2, Mose_3, Mose_4, Mose_5],
        [
            Josua,
            Richter,
            Ruth,
            Samuel_1,
            Samuel_2,
            Könige_1,
            Könige_2,
            Chronik_1,
            Chronik_2,
            Esra,
            Nehemia,
            Esther,
        ],
        [Hiob, Psalmen, Sprüche, Prediger, Hohelied],
        [Jesaja, Jeremia, Klagelieder, Hesekiel, Daniel],
        [
            Hosea,
            Joel,
            Amos,
            Obadja,
            Jona,
            Micha,
            Nahum,
            Habakuk,
            Zephanja,
            Haggai,
            Sacharja,
            Maleachi,
        ],
        [Matthäus, Markus, Lukas, Johannes],
        [Apostelgeschichte],
        [
            Römer,
            Korinther_1,
            Korinther_2,
            Galater,
            Epheser,
            Philipper,
            Kolosser,
            Thessalonicher_1,
            Thessalonicher_2,
            Timotheus_1,
            Timotheus_2,
            Titus,
            Philemon,
            Hebräer,
            Jakobus,
            Petrus_1,
            Petrus_2,
            Johannes_1,
            Johannes_2,
            Johannes_3,
            Judas,
        ],
        [Offenbarung],
    ];

    // logic
    let started = false;
    let current_headings = [];
    let current_heading = null;
    let current_guess = 0;

    // stats
    let correct_guesses = 0;
    let number_of_all_headings = 0;

    let dialog = undefined;

    /**
     * @param {any[]} a
     */
    function shuffle(a) {
        const b = [...a];
        for (let i = b.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [b[i], b[j]] = [b[j], b[i]];
        }
        return b;
    }

    function selectAll(section) {
        for (let book of section) {
            book.selected = true;
        }
        return section;
    }

    function start() {
        started = true;
        current_headings = shuffle(
            books
                .flat()
                .filter((book) => book.selected)
                .flatMap((book) => book.headings),
        );
        if (current_headings.length <= 0) {
            started = false;
            return;
        }
        number_of_all_headings = current_headings.length;
        current_heading = current_headings.pop();
        correct_guesses = 0;
    }

    function checkOption(clickedHeading, button) {
        if (clickedHeading.heading == current_heading.heading) {
            let false_buttons = document.getElementsByClassName("false");
            Array.from(false_buttons).forEach((btn) => btn.classList.remove("false"));

            button.disabled = true;
            button.classList.add("correct-" + current_guess);

            const heading_text = document.createTextNode(
                current_heading.heading,
            );
            const heading_line = document.createElement("div");
            heading_line.appendChild(heading_text);

            button.appendChild(heading_line);
            if (current_guess == 0) {
                correct_guesses += 1;
            }
            current_guess = 0;
            current_heading = current_headings.pop();
        } else if (current_guess >= 3) {
            /**
             * @type NodeListOf<HTMLButtonElement>
             */
            let all_buttons = document.querySelectorAll("button.heading-option");
            let correct_button = Array.from(all_buttons).filter(
                (btn) =>
                    !btn.disabled &&
                    btn.dataset.heading ==
                        current_heading.heading.replaceAll(" ", "_"),
            )[0];
            correct_button.classList.add("false");
            current_guess = 4;
        } else {
            current_guess += 1;
        }
        if (!current_heading) {
            dialog.showModal();
        }
    }

    function endTraining() {
        started = false;
        dialog.close();
    }
</script>

{#if !started}
    <h1>Bibelüberschriften Trainer</h1>
    <div id="book-box">
        {#each books as section}
            <div class="book-section">
                <button
                    class="select-all"
                    on:click={() => (section = selectAll(section))}
                    >Alle auswählen</button
                >
                {#each section as book}
                    <div class="book">
                        <input type="checkbox" bind:checked={book.selected} />
                        <span>{book.name}</span>
                    </div>
                {/each}
            </div>
        {/each}
    </div>
    <button on:click={start}>Start</button>
{:else}
    {#if current_heading}
        <div id="current-heading">{current_heading.heading}</div>
    {/if}
    <div id="book-box">
        {#each books.flat().filter((book) => book.selected) as book}
            <div class="book-section">
                <h2>{book.name}</h2>
                {#each book.headings as heading}
                    <div class="heading-option">
                        <button
                            class="heading-option"
                            data-heading={heading.heading.replaceAll(" ", "_")}
                            on:click={(e) => checkOption(heading, e.target)}
                        >
                            {heading.start.chapter}:{heading.start.verse} - {heading
                                .end.chapter}:{heading.end.verse}
                        </button>
                    </div>
                {/each}
            </div>
        {/each}
    </div>
    <button
        on:click={() => {
            dialog.showModal();
        }}>Übung Beenden</button
    >
    <dialog bind:this={dialog}>
        <h2>Übung beendet</h2>
        <div>
            <span>{correct_guesses}/{number_of_all_headings}</span>
            <span>
                {Math.round((correct_guesses / number_of_all_headings) * 100)}%
            </span>
        </div>
        <button on:click={endTraining}>Zurück zur Auswahl</button>
    </dialog>
{/if}

<style>
    #book-box {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
    }

    .book-section {
        padding: 1em;
        background: #202020;
        border-radius: 8px;
        margin: 1em;
        width: max-content;
    }

    .book {
        width: max-content;
    }

    .select-all {
        width: max-content;
        margin-bottom: 1em;
    }

    .heading-option {
        margin: 0.5em;
    }

    #current-heading {
        position: sticky;
        top: 1em;
        padding: 1em;
        background: #303030;
        border-radius: 8px;
    }

    @keyframes blink {
        0% {
            background: #1a1a1a;
        }
        50% {
            background: #85251a;
        }
        100% {
            background: #1a1a1a;
        }
    }

    :global(.false) {
        animation-name: blink;
        animation-duration: 0.5s;
        animation-iteration-count: infinite;
    }

    :global(.correct-0) {
        background: #33671a;
    }
    :global(.correct-1) {
        background: #8d9916;
    }
    :global(.correct-2) {
        background: #d0a42e;
    }
    :global(.correct-3) {
        background: #b05623;
    }
    :global(.correct-4) {
        background: #85251a;
    }

    dialog {
        position: relative;
        border-radius: 8px;
    }

    dialog > div {
        margin: 1em;
        display: flex;
        justify-content: space-between;
        gap: 2em;
        font-size: 2em;
    }
</style>
