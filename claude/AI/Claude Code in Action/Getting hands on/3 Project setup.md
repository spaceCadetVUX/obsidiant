Working with Claude Code is more interesting if you have a project to work with.

I've put together a small project to explore with Claude Code. It is the same UI generation app shown in a previous video. **Note:** you don't have to run this project. You can always follow along with the remainder of the course with your own code base if you wish!

**Setup**

This project requires a small amount of setup:

1. Ensure you have Node JS installed locally. [Link to installation directions](https://nodejs.org/en/download).
2. Download the zip file called `uigen.zip` attached to this lecture and extract it
3. In the project directory, run `npm run setup` to install dependencies and set up a local SQLite database
4. **Optional:** this project uses Claude through the Anthropic API to generate UI components. If you want to fully test out the app, you will need to provide an API key to access the Anthropic API. _This is optional. If no API key is provided, the app will still generate some static fake code._ Here's how you can set the api key:
    1. Get an Anthropic API key at [https://console.anthropic.com/](https://console.anthropic.com/)
    2. Place your API key in the `.env` file.
5. Start the project by running `npm run dev`

#### Downloads

- [uigen.zip](https://cc.sj-cdn.net/instructor/4hdejjwplbrm-anthropic/assets/1769622681/uigen.zip?response-content-disposition=attachment&Expires=1773226902&Signature=li3q6GOIHK7FXnAsPMWI7d9IJM7BRel9cn~CSv8FV5sM2Y8kSxRVbnwoUJlDOf46Xyx5E3NLAx5AW3-2e6dzemRRo0HPGd7IiXxt1yaFan9jAHNdnKdxbKlp9AZcVKT8AQjaNF1QUHdOu0WT9ZG5iYckHYlvRdZoK6nltIRl7XoaM6psFsr06ELs42q4DOTCrYJFM3lV1FnDDkAQzhoN16yIeaLjJptuE2IJxWWAmWAGxtnlra-C31Ny~fGEds1bYg9o6XLV8LhgWmLsahpxwiKZnd3An5QmSo5XGCipjWM0WB4wCKH5RPv9W-or8Vpp203JmGq8udt44mnr4-ic5g__&Key-Pair-Id=APKAI3B7HFD2VYJQK4MQ)
