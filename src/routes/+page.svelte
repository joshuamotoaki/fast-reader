<script lang="ts">
let currentWord: string = "";   // Current word being displayed
let textSpeed: number = 250;    // Speed of text in words per minute
let isActive: boolean = false;  // Whether the text stream is active

let textInput: string = "";     // Text input from user
let textArray: string[] = [];   // Array of words from text input

let index = 0;                  // Index of current word in text array

/**
 * Starts the text stream
 */
const handleGo = () => {
    textArray = textInput.split(" ");
    index = 0;
    isActive = true;
    startTextStream();
}

/**
 * Stops the text stream
 */
const handleStop = () => {
    isActive = false;
}

/**
 * Resumes the text stream
 */
const handleResume = () => {
    isActive = true;
    startTextStream();
}

/**
 * Begin the text stream
 */
const startTextStream = () => {
    // If the text stream is active
    if (isActive) {
        // If the text array is not empty
        if (index < textArray.length) {
            currentWord = textArray[index];
            index++;

            // Wait for the specified amount of time
            setTimeout(startTextStream, 60000 / textSpeed);
        } else {
            // If the text array is empty, stop the text stream
            currentWord = "";
            isActive = false;
        }
    }
}

/**
 * Resets the text input and current word
 */
const handleReset = () => {
    textInput = "";
    currentWord = "";
    isActive = false;
    textArray = [];
    index = 0;
}
</script>

<main class="h-screen w-screen">
    <div class="navbar bg-base-300">
        <div class="flex-1">
          <a class="btn btn-ghost normal-case text-xl" href="/">Fast Reader</a>
        </div>
        <div class="flex-none">
          <ul class="menu menu-horizontal px-1">
            <!-- <li><a>Link</a></li>
            <li>
              <details>
                <summary>
                  Parent
                </summary>
                <ul class="p-2 bg-base-100">
                  <li><a>Link 1</a></li>
                  <li><a>Link 2</a></li>
                </ul>
              </details>
            </li> -->
          </ul>
        </div>
    </div>

    <div class="mockup-window border border-base-300 w-[600px] max-w-screen 
    mx-auto mt-12">
        <div class="flex justify-center px-4 py-16 border-t border-base-300
        text-4xl">
            {currentWord}
        </div>
    </div>

    <div class="w-fit mx-auto mt-12">
        <textarea class="textarea textarea-bordered w-[600px] max-w-screen
        h-40"
        bind:value={textInput}
        placeholder="Enter Text" />
    </div>

    <div class="mt2 w-[600px] max-w-screen mx-auto space-x-2">
        <input type="number" placeholder="Speed" step="50" min="50" max="1000"
        class="input input-bordered max-w-xs" 
        bind:value={textSpeed}/>

        <button class="btn btn-outline btn-primary"
        on:click={handleGo}>
            Go
        </button>
        
        <button class="btn btn-outline btn-secondary"
        on:click={handleStop}>
            Stop
        </button>

        <button class="btn btn-outline btn-secondary"
        on:click={handleResume}>
            Resume
        </button>

        <button class="btn btn-outline"
        on:click={handleReset}>
            Reset
        </button>
    </div>

    <footer class="footer footer-center p-4 bg-base-300 text-base-content
    absolute bottom-0">
        <aside>
          <p>A Piece of The Synapse Project 2023</p>
        </aside>
      </footer>
</main>

<style lang="postcss">

</style>