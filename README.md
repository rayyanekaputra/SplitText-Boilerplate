# SplitText-Boilerplate
***Not a Plugin. ***An Alternative to SplitText by GSAP and How to Use Them in with jQuery

If you're looking for a simple, jQuery-based alternative to GSAP's SplitText() for breaking up your text into characters, words, or lines, you're in the right place! This is a lightweight, no-frills way to split text for easy animations or styling. And guess what? It's free and open-source!

### All you have to do, just copy paste!

## Features ✨
- Split text into **chars**, **words**, or **lines**.
- Super easy to use with **GSAP** or just plain CSS.
- **No plugin needed** — just jQuery and some simple code.
- Open-source and free to use (yay!).

```javascript
 function splitText($element, type) {
      const originalText = $element.text();
      const lines = [];

      // Helper: Wrap text in a span
      const wrapText = (text, className) => `<span class="${className}">${text}</span>`;

      if (type === 'chars') {
        $element.html(
          originalText
            .split('')
            .map(char => wrapText(char === ' ' ? '&nbsp;' : char, 'char'))
            .join('')
        );
      } else if (type === 'words') {
        $element.html(
          originalText
            .split(' ')
            .map(word => wrapText(word, 'word'))
            .join(' ')
        );
      } else if (type === 'lines') {
        const words = originalText.split(' ');
        $element.html(
          words.map(word => wrapText(word, 'word')).join(' ')
        );

        const tempLines = [];
        $element.children('.word').each(function () {
          const $word = $(this);
          const top = $word.offset().top;
          if (!tempLines.length || tempLines[tempLines.length - 1].top !== top) {
            tempLines.push({ top, words: [] });
          }
          tempLines[tempLines.length - 1].words.push($word[0].outerHTML);
        });

        tempLines.forEach(line => {
          lines.push(line.words.join(' '));
        });

        $element.html(lines.map(line => wrapText(line, 'line')).join(''));
      }
    }

```

## How to Use it 🏃‍♂️💨
Basic Steps:
1. Add jQuery and GSAP to your project.
2. Drop the splitText() function into your script.
3. Call splitText() on your text element and choose how you want to split it: 'chars', 'words', or 'lines'.
4. ***Remember that splitText() only accepts jQuery object, so don't get confused with Javascript DOM.*** jquery: $('.text') !=== vanillajs: querySelectorAll('.text')
```javascript
const $textElement = $('#text');
splitText($textElement, 'chars'); // Options: 'chars', 'words', 'lines'
```

## Example Usage
``` HTML
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SplitText Boilerplate</title>
  <script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
  <style>
    .char, .word, .line {
      display: inline-block;
    }

    .line {
      display: block;
    }
  </style>
</head>

<body>
  <div id="text" style="width: 300px; font-size: 24px; line-height: 1.5;">
    Check out this fun jQuery-based SplitText example! 🎉
  </div>

  <script>
    /**
     * Splits your text into chars, words, or lines with jQuery. 🎉
     * @param {jQuery} $element - The jQuery element containing the text.
     * @param {string} type - Choose 'chars', 'words', or 'lines' to split the text.
     */
    function splitText($element, type) {
      const originalText = $element.text();
      const lines = [];

      // Helper to wrap text in a span
      const wrapText = (text, className) => `<span class="${className}">${text}</span>`;

      if (type === 'chars') {
        $element.html(
          originalText
            .split('')
            .map(char => wrapText(char === ' ' ? '&nbsp;' : char, 'char'))
            .join('')
        );
      } else if (type === 'words') {
        $element.html(
          originalText
            .split(' ')
            .map(word => wrapText(word, 'word'))
            .join(' ')
        );
      } else if (type === 'lines') {
        const words = originalText.split(' ');
        $element.html(
          words.map(word => wrapText(word, 'word')).join(' ')
        );

        const tempLines = [];
        $element.children('.word').each(function () {
          const $word = $(this);
          const top = $word.offset().top;
          if (!tempLines.length || tempLines[tempLines.length - 1].top !== top) {
            tempLines.push({ top, words: [] });
          }
          tempLines[tempLines.length - 1].words.push($word[0].outerHTML);
        });

        tempLines.forEach(line => {
          lines.push(line.words.join(' '));
        });

        $element.html(lines.map(line => wrapText(line, 'line')).join(''));
      }
    }

    // Call the function on your text element
    const $textElement = $('#text');
    splitText($textElement, 'chars'); // Split it however you like: 'chars', 'words', 'lines'

    // Fun with animations (because why not? 🎨)
    $('#text .char').each(function () {
      $(this).on('mouseenter', function () {
        console.log("Hey, you're in: " + $(this).text());
        gsap.to(this, { color: 'green' });
      });

      $(this).on('mouseleave', function () {
        console.log("Whoops, you're leaving: " + $(this).text());
        gsap.to(this, { color: '#4e4e4e' });
      });
    });
  </script>
</body>

</html>
```

## Available Options 🤓
- 'chars': Breaks the text into individual characters. Perfect for character-based animations!
- 'words': Breaks the text into words. Great for word-based animations or effects.
- 'lines': Breaks the text into lines. Use this for line-by-line text animations.

## Contributing 👐
Feel free to fork it, play around with it, and make it better! Pull requests are welcome, and so are ideas, issues, and all that good stuff.
