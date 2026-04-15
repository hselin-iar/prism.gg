# prism.gg

A simple web game to test how bad human memory actually is when it comes to color recall. 

[[Link to play the game](https://prismgg.vercel.app/)]

### The Idea
You get shown a target color for exactly 600 milliseconds. After that, it disappears, and you have to recreate that exact shade from memory using Hue, Saturation, and Brightness (HSB) sliders. You do this for 5 rounds, and get a score out of 50 based on your accuracy. 

### How it works & Building the frontend
I built this purely with vanilla HTML, CSS, and JS—no frameworks or build steps. 

When figuring out how to score the game, it quickly became obvious that simply comparing the RGB values of the target color and the guessed color wouldn't work. Human vision doesn't process RGB linearly, so an RGB difference doesn't actually reflect how "close" two colors look to the human eye. 

To solve this, the game's logic relies on HSB (Hue, Saturation, Brightness).
*   **Integrating Perceptual Scoring:** Instead of writing complex color-space math from scratch, I integrated an algorithm that calculates the Euclidean distance between two colors on a cylindrical coordinate system (which handles the fact that Hue wraps around from 360° back to 0°). 
*   **Score Mapping & State:** The real challenge was taking the raw output from that distance algorithm and mapping it into a fair, playable score out of 10.00 for each round. I set up a dynamic feedback system that reads this final score and updates the UI dialogue state based on specific accuracy thresholds.
*   **UI/Slider Syncing:** Getting the custom DOM sliders to feel responsive while constantly updating the active background colors and retaining the HSB values without lag took some careful event listener management.

### Running it locally
There's no build process. Just clone the repo and double-click `index.html` to play.

```bash
git clone https://github.com/yourusername/prism.gg.git
