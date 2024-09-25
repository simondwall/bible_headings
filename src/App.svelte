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
        { title: "Tora", books: [Mose_1, Mose_2, Mose_3, Mose_4, Mose_5] },
        {
            title: "Geschichtsbücher",
            books: [
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
        },
        {
            title: "Lehr- und Poesiebücher",
            books: [Hiob, Psalmen, Sprüche, Prediger, Hohelied],
        },
        {
            title: "Große Propheten",
            books: [Jesaja, Jeremia, Klagelieder, Hesekiel, Daniel],
        },
        {
            title: "Kleine Propheten",
            books: [
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
        },
        { title: "Evangelien", books: [Matthäus, Markus, Lukas, Johannes] },
        { title: "Geschichtsbuch", books: [Apostelgeschichte] },
        {
            title: "Briefe",
            books: [
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
        },
        { title: "Apokalyptisches Buch", books: [Offenbarung] },
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

    function start() {
        started = true;
        current_headings = shuffle(
            books
                .flatMap((section) => section.books)
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
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    function checkOption(clickedHeading, button) {
        if (clickedHeading.heading == current_heading.heading) {
            let false_buttons = document.getElementsByClassName("false");
            Array.from(false_buttons).forEach((btn) =>
                btn.classList.remove("false"),
            );

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
            let all_buttons = document.querySelectorAll(
                "button.heading-option",
            );
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
    <main>
        <div class="grid">
            {#each books as section}
                <div class="card">
                    <h1 class="title">{section.title}</h1>
                    <div class="list">
                        {#each section.books as book}
                            <div class="book">
                                <input
                                    id="{book.name}-checkbox"
                                    type="checkbox"
                                    bind:checked={book.selected}
                                />
                                <label for="{book.name}-checkbox"
                                    >{book.name}</label
                                >
                            </div>
                        {/each}
                    </div>
                </div>
            {/each}
        </div>
    </main>

    <div class="sticky footer">
        <button class="primary" on:click={start}>Start</button>
    </div>
{:else}
    {#if current_heading}
        <div class="sticky header">
            <h1 class="title">{current_heading.heading}</h1>
        </div>
    {/if}

    <main>
        <div class="grid">
            {#each books
                .flatMap((section) => section.books)
                .flat()
                .filter((book) => book.selected) as book}
                <div
                    class="card"
                    style="width: 80%; max-width: 25em; margin: auto;"
                >
                    <h1 class="title">{book.name}</h1>
                    <div class="list">
                        {#each book.headings as heading}
                            <button
                                style="width: 100%; text-wrap:wrap;"
                                class="heading-option"
                                data-heading={heading.heading.replaceAll(
                                    " ",
                                    "_",
                                )}
                                on:click={(e) => checkOption(heading, e.target)}
                            >
                                {heading.start.chapter}:{heading.start.verse} - {heading
                                    .end.chapter}:{heading.end.verse}
                            </button>
                        {/each}
                    </div>
                </div>
            {/each}
        </div>

        <dialog bind:this={dialog}>
            <div class="card">
                <h1 class="title">Übung beendet</h1>
                <div style="width: max-content; margin: auto;">
                    {correct_guesses}/{number_of_all_headings}
                </div>
                <div style="width: max-content; margin: auto;">
                    {Math.round(
                        (correct_guesses / number_of_all_headings) * 100,
                    )}%
                </div>
                <button class="primary" on:click={endTraining}
                    >Zurück zur Auswahl</button
                >
            </div>
        </dialog>
    </main>

    <div class="sticky footer">
        <button
            class="primary"
            on:click={() => {
                dialog.showModal();
            }}>Übung Beenden</button
        >
    </div>
{/if}

<style>
    @keyframes blink {
        0% {
            background: #85251a00;
        }
        50% {
            background: #85251a;
        }
        100% {
            background: #85251a00;
        }
    }

    :global(
            .false,
            .correct-0,
            .correct-1,
            .correct-2,
            .correct-3,
            .correct-4
        ) {
        position: relative;
    }
    :global(
            .false::before,
            .correct-0::before,
            .correct-1::before,
            .correct-2::before,
            .correct-3::before,
            .correct-4::before
        ) {
        position: absolute;
        top: -3.5px;
        left: -3.5px;
        content: "";
        width: 15px;
        height: 15px;
        border-radius: 7.5px;
    }

    :global(.false::before) {
        animation-name: blink;
        animation-duration: 0.5s;
        animation-iteration-count: infinite;
    }
    :global(.correct-0::before) {
        background: #33671a;
    }
    :global(.correct-1::before) {
        background: #8d9916;
    }
    :global(.correct-2::before) {
        background: #d0a42e;
    }
    :global(.correct-3::before) {
        background: #b05623;
    }
    :global(.correct-4::before) {
        background: #85251a;
    }
</style>
