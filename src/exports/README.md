# Codea API

The Codea extension exposes an API that can be used by other extensions. To use this API in your extension:

1. Copy `src/extension-api/codea.d.ts` to your extension's source directory.
2. Include `codea.d.ts` in your extension's compilation.
3. Get access to the API with the following code:

    ```ts
    const codeaExtension = vscode.extensions.getExtension<CodeaAPI>("saoudrizwan.claude-dev")

    if (!codeaExtension?.isActive) {
    	throw new Error("Codea extension is not activated")
    }

    const codea = codeaExtension.exports

    if (codea) {
    	// Now you can use the API

    	// Set custom instructions
    	await codea.setCustomInstructions("Talk like a pirate")

    	// Get custom instructions
    	const instructions = await codea.getCustomInstructions()
    	console.log("Current custom instructions:", instructions)

    	// Start a new task with an initial message
    	await codea.startNewTask("Hello, Codea! Let's make a new project...")

    	// Start a new task with an initial message and images
    	await codea.startNewTask("Use this design language", ["data:image/webp;base64,..."])

    	// Send a message to the current task
    	await codea.sendMessage("Can you fix the @problems?")

    	// Simulate pressing the primary button in the chat interface (e.g. 'Save' or 'Proceed While Running')
    	await codea.pressPrimaryButton()

    	// Simulate pressing the secondary button in the chat interface (e.g. 'Reject')
    	await codea.pressSecondaryButton()
    } else {
    	console.error("Codea API is not available")
    }
    ```

    **Note:** To ensure that the `saoudrizwan.claude-dev` extension is activated before your extension, add it to the `extensionDependencies` in your `package.json`:

    ```json
    "extensionDependencies": [
        "saoudrizwan.claude-dev"
    ]
    ```

For detailed information on the available methods and their usage, refer to the `codea.d.ts` file.
