from PIL import Image
import glob

def create_capybara_gif(output_filename="ngoc_capybara.gif", duration_ms=200):
    # Use glob to find all images, assuming they are named predictably (e.g., capy01.png, capy02.png)
    # The 'sorted' function ensures they are processed in order
    image_paths = sorted(glob.glob("capy*.png")) 

    if not image_paths:
        print("Error: No images found matching 'capy*.png'.")
        return

    # Load all images using Pillow
    images = [Image.open(path) for path in image_paths]

    # Save the first image, appending the rest as frames
    images[0].save(
        output_filename,
        save_all=True,
        append_images=images[1:],
        duration=duration_ms, 
        loop=0
    )
    print(f"GIF '{output_filename}' created successfully!")

if __name__ == "__main__":
    # Ensure you have images named like capy01.png, capy02.png, etc., in your folder
    create_capybara_gif()
