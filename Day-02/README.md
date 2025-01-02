**Day02**

Blog :

Discord :

Install required Dependencies 
```
pip install requests python-pptx
```

Code

```
import os
import requests
from pptx import Presentation
from pptx.util import Inches

def download_image(query, filename):
    url = f"https://source.unsplash.com/featured/?{query}"
    response = requests.get(url)
    if response.status_code == 200:
        with open(filename, 'wb') as f:
            f.write(response.content)
        return filename
    return None

def add_slide(prs, title, content, image_query=None):
    # Choose a layout that includes at least two placeholders
    for layout in prs.slide_layouts:
        if len(layout.placeholders) > 1:
            slide_layout = layout
            break
    slide = prs.slides.add_slide(slide_layout)
    title_placeholder = slide.shapes.title
    content_placeholder = slide.placeholders[1]  # Ensure this placeholder exists in the layout

    title_placeholder.text = title

    tf = content_placeholder.text_frame
    tf.text = content[0]  # Set the first line of content

    for line in content[1:]:
        p = tf.add_paragraph()
        p.text = line

    if image_query:
        image_filename = f"{image_query.replace(' ', '_')}.jpg"
        image_path = download_image(image_query, image_filename)
        if image_path:
            left = Inches(5)  # Position on the right side of the slide
            top = Inches(1)
            height = Inches(4.5)
            slide.shapes.add_picture(image_path, left, top, height=height)
            os.remove(image_path)  # Clean up the image file after adding to slide

def create_kubernetes_presentation():
    prs = Presentation()

    # Title Slide
    slide_layout = prs.slide_layouts[0]  # Title slide layout
    slide = prs.slides.add_slide(slide_layout)
    title = slide.shapes.title
    subtitle = slide.placeholders[1]

    title.text = "Kubernetes Learning Journey"
    subtitle.text = "A Comprehensive Guide to Mastering Kubernetes"

    # Slides for different sections
    slides_content = [
        ("Introduction to Kubernetes", [
            "Kubernetes is a leading technology in cloud computing.",
            "Supports complex applications on various architectures.",
            "Requires knowledge of containers, YAML, and more."
        ], "Kubernetes"),
        ("Learning Materials Overview", [
            "Designed for diverse backgrounds: beginners to experts.",
            "Series of materials targeting specific audiences and topics."
        ], "education"),
        ("Core Concepts", [
            "Overview of cluster architecture.",
            "Introduction to API primitives.",
            "Basics: Pods, ReplicaSets, Deployments, Services."
        ], "Kubernetes architecture"),
        ("Beginner-Level Content", [
            "For newcomers without prior experience in containers or orchestration.",
            "High-level overview and basic lab setup.",
            "Core concepts for deploying applications."
        ], "beginner learning"),
        ("Advanced Administrator Topics", [
            "Deploying high-availability clusters.",
            "Scheduling, monitoring, maintenance, security, storage, and troubleshooting."
        ], "Kubernetes administrator"),
        ("Developer-Focused Content", [
            "Designing, building, and configuring cloud-native applications.",
            "Topics: ConfigMaps, secrets, service accounts, multi-container pods, and more."
        ], "cloud native development"),
        ("Practical Exercises and Quizzes", [
            "Hands-on exercises to practice deploying applications.",
            "Quizzes to reinforce learning and understanding."
        ], "Kubernetes training"),
        ("Flexible Learning Path", [
            "Choose focus: administration or development.",
            "Structured to build knowledge progressively."
        ], "flexible learning")
    ]

    for title, content, image_query in slides_content:
        add_slide(prs, title, content, image_query)

    prs.save('Kubernetes_Learning_Journey.pptx')

if __name__ == "__main__":
    create_kubernetes_presentation()
```

Run Script 
```
python your_script_name.py
```
