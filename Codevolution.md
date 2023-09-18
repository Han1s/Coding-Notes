# Design Tips for Developers

### III. How to handle Image Quirks

- unreadable text

  - move the text away from the image sometimes

  - add overlay that contrasts with the text and reduce its height to contrast only the text using gradient (starts where the text is and ends at the top)

  - ```css
    position: absolute,
    width: 360px
    height: 186px
    left: 188px
    top: 600px
    
    background: linear-gradient(180deg, rgba(0, 0, 0, 0.001) 0%, #000000 100%);
    mix-blend-mode: normal;
    opacity: 0.6
    ```

- when working with avatars

  - hard to distinguish from the background sometimes

  - add the inset-shadow to the image

  - ```css
    position: absolute;
    width: 160px;
    height: 160px
    background: url(.png);
    box-shadow: inset 0px 1px 2px rgba(0, 0, 0, 0.25);
    ```

    

