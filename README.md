import tkinter as tk
from tkinter import messagebox
from tkinter import filedialog
import qrcode
from PIL import Image

# Function to generate QR code
def generate_qr():
    data = entry.get()
    if not data:
        messagebox.showwarning("Input Error", "Please enter data for the QR code.")
        return
    
    # Generate the QR code
    qr = qrcode.QRCode(version=1, box_size=10, border=5)
    qr.add_data(data)
    qr.make(fit=True)
    
    # Create the QR code image
    img = qr.make_image(fill='black', back_color='white')
    
    # Display the image in the window
    img.show()

# Function to save the QR code as PNG
def save_qr():
    data = entry.get()
    if not data:
        messagebox.showwarning("Input Error", "Please enter data for the QR code.")
        return

    # Generate the QR code
    qr = qrcode.QRCode(version=1, box_size=10, border=5)
    qr.add_data(data)
    qr.make(fit=True)
    
    # Create the QR code image
    img = qr.make_image(fill='black', back_color='white')
    
    # Open the file save dialog
    file_path = filedialog.asksaveasfilename(defaultextension=".png", filetypes=[("PNG files", "*.png")])
    
    if file_path:
        img.save(file_path)
        messagebox.showinfo("Success", f"QR code saved as {file_path}")
    else:
        messagebox.showwarning("Save Error", "No file path selected.")

# Create the main window
root = tk.Tk()
root.title("QR Code Generator")
root.geometry("400x300")

# Create and place the components
label = tk.Label(root, text="Enter text for QR Code:")
label.pack(pady=10)

entry = tk.Entry(root, width=40)
entry.pack(pady=10)

generate_button = tk.Button(root, text="Generate QR Code", command=generate_qr)
generate_button.pack(pady=5)

save_button = tk.Button(root, text="Save QR Code", command=save_qr)
save_button.pack(pady=5)

# Run the Tkinter event loop
root.mainloop()# QR-code-generator
