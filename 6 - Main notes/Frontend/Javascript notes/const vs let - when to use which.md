
2025-07-06 19:10

Status: #ReadLater 

Tags: [Read later](3%20-%20Tags/Read%20later.md) [React](3%20-%20Tags/React.md)

---
# const vs let - when to use which

```jsx
export default function AssemblyEndgame() {

    const [currentWord, setCurrentWord] = useState("react") // why is const being used here

    const []

    const alphabet = "abcdefghijklmnopqrstuvwxyz"

  

    const languageElements = languages.map(lang => {

        const styles = {

            backgroundColor: lang.backgroundColor,

            color: lang.color

        }

        return (

            <span

                className="chip"

                style={styles}

                key={lang.name}

            >

                {lang.name}

            </span>

        )

    })

    const letterElements = currentWord.split("").map((letter, index) => (

        <span key={index}>{letter.toUpperCase()}</span>

    ))

    const keyboardElements = alphabet.split("").map(letter => (

        <button key={letter}>{letter.toUpperCase()}</button>

    ))

  

    return (

        <main>

            <header>

                <h1>Assembly: Endgame</h1>

                <p>Guess the word within 8 attempts to keep the

                programming world safe from Assembly!</p>

            </header>

            <section className="game-status">

                <h2>You win!</h2>

                <p>Well done! 🎉</p>

            </section>

            <section className="language-chips">

                {languageElements}

            </section>

            <section className="word">

                {letterElements}

            </section>

            <section className="keyboard">

                {keyboardElements}

            </section>

            <button className="new-game">New Game</button>

        </main>

    )

}
```

---
## References