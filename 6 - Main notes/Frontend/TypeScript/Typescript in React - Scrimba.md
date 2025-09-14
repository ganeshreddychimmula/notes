
2025-09-13 02:49

Status:

Tags: [TypeScript](../../../3%20-%20Tags/TypeScript.md)

---
# Typescript in React - Scrimba

- Typing useState
```ts
const [currentWord, setCurrentWord] = useState<string>(():string => getRandomWord())
```

- React component type - `JSX.Element`
```ts
import type {JSX} from 'react'  

export default function Header():JSX.Element {

    return (

        <header>

            <h1>Assembly: Endgame</h1>

            <p>Guess the word within 8 attempts to keep the

                programming world safe from Assembly!</p>

        </header>

    )

}
```

```tsx
import type {JSX} from 'react'


type AriaLiveStatusProps = {

    currentWord:string,

    lastGuessedLetter:string,

    guessedLetters:string[],

    numGuessesLeft:number

}

  

export default function AriaLiveStatus({

                                           currentWord,

                                           lastGuessedLetter,

                                           guessedLetters,

                                           numGuessesLeft

                                       }:AriaLiveStatusProps):JSX.Element {

    return (

        <section

            className="sr-only"

            aria-live="polite"

            role="status"

        >

            <p>

                {currentWord.includes(lastGuessedLetter) ?

                    `Correct! The letter ${lastGuessedLetter} is in the word.` :

                    `Sorry, the letter ${lastGuessedLetter} is not in the word.`

                }

                You have {numGuessesLeft} attempts left.

            </p>

            <p>

                Current word: {currentWord.split("").map((letter:string):string =>

                guessedLetters.includes(letter) ? letter + "." : "blank."

            ).join(" ")}

            </p>

        </section>

    )

}
```
---
## References