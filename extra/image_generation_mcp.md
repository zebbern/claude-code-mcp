
# Image Generation MCP

The Image Generation MCP allows Claude Code to generate images based on textual descriptions or other inputs, leveraging various AI image generation models. This enables Claude to create visual assets, prototypes, or illustrations directly from your instructions, enhancing creative and design workflows.

## Capabilities

*   **Text-to-Image Generation**: Create images from natural language prompts.
*   **Image-to-Image Generation**: Modify existing images or create variations based on a reference image and a prompt.
*   **Style Transfer**: Apply artistic styles from one image to another.
*   **Model Integration**: Supports integration with different image generation models (e.g., DALL-E, Stable Diffusion, Midjourney).

## Configuration

To add the Image Generation MCP, you typically use `npx` to run the official server. You will likely need API keys or credentials for the underlying image generation service.

```bash
claude mcp add image-gen-server --command npx --args -y @modelcontextprotocol/server-image-generation --env IMAGE_GEN_API_KEY=<YOUR_API_KEY>
```

*   Replace `<YOUR_API_KEY>` with your actual image generation service API key.

### Example Configuration in `.mcp.json` (Project Scope)

```json
{
  "mcpServers": {
    "image-generation": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-image-generation"
      ],
      "env": {
        "IMAGE_GEN_API_KEY": "<YOUR_API_KEY>"
      }
    }
  }
}
```

## Usage Examples

Once configured, Claude can use the Image Generation MCP to create images.

### 1. Generating an Image from Text

Ask Claude to generate an image based on a description:

```
Generate an image of "a futuristic city at sunset, cyberpunk style, with flying cars and neon lights".
```

Claude will generate the image and provide a link or embed it in the conversation.

### 2. Creating an Image Variation

Instruct Claude to create a variation of an existing image:

```
Create a variation of the image at @filesystem:file:///path/to/my/image.png, making it "more vibrant and adding a touch of magic".
```

Claude will use the provided image as a reference and generate a new one based on the prompt.

### 3. Applying a Style

Ask Claude to apply a specific artistic style to an image:

```
Apply a "watercolor painting style" to the image at @filesystem:file:///path/to/my/photo.jpg.
```

Claude will transform the image into the specified style.

## Best Practices

*   **API Key Security**: Protect your image generation API keys. Use environment variables or a secure secrets management system.
*   **Prompt Engineering**: Experiment with different prompts to achieve the desired image results. Be descriptive and specific.
*   **Ethical Considerations**: Be mindful of ethical guidelines and potential biases in AI image generation.
*   **Cost Management**: Be aware of the costs associated with image generation APIs, as they can vary per model and usage.

For more details, refer to the [official Image Generation MCP documentation](https://modelcontextprotocol.io/examples/image-generation).

