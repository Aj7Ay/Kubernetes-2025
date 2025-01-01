**Blog** : [https://mrcloudbook.com](https://mrcloudbook.com/kubernetes-day-01-cka-2025/)

**DAY 01**

**Install Required Packages**

```
pip install requests python-pptx
```

Use this Script to Generate PPT ( SIMPLE ONE )

```
import os
import requests
from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.enum.text import PP_ALIGN

def download_image(query, filename):
    url = f"https://source.unsplash.com/featured/?{query}"
    response = requests.get(url)
    if response.status_code == 200:
        with open(filename, 'wb') as f:
            f.write(response.content)
        return filename
    return None

def add_title_slide(prs, title, subtitle):
    title_slide_layout = prs.slide_layouts[0]
    slide = prs.slides.add_slide(title_slide_layout)
    title_shape = slide.shapes.title
    subtitle_shape = slide.placeholders[1]

    title_shape.text = title
    subtitle_shape.text = subtitle

def add_content_slide(prs, title, content, image_query):
    bullet_slide_layout = prs.slide_layouts[1]
    slide = prs.slides.add_slide(bullet_slide_layout)
    shapes = slide.shapes

    title_shape = shapes.title
    body_shape = shapes.placeholders[1]

    title_shape.text = title

    tf = body_shape.text_frame
    tf.text = content[0]

    for bullet_point in content[1:]:
        p = tf.add_paragraph()
        p.text = bullet_point
        p.level = 1

    if image_query:
        image_filename = f"{image_query.replace(' ', '_')}.jpg"
        image_path = download_image(image_query, image_filename)
        if image_path:
            left = Inches(7)  # Adjust as needed
            top = Inches(2)   # Adjust as needed
            width = Inches(3) # Adjust as needed
            slide.shapes.add_picture(image_path, left, top, width=width)
            os.remove(image_path)  # Clean up the image file after adding to slide

def create_presentation():
    prs = Presentation()

    # Title Slide
    add_title_slide(prs, "Certified Kubernetes Administrator Course", "Presenter: Mr. Cloud Book")

    # Introduction Slides
    intro_slides = [
        ("What is Kubernetes?", [
            "Open-source container orchestration platform",
            "Automates deployment, scaling, and management of containerized applications",
            "Originally developed by Google, now maintained by CNCF",
            "Provides a robust ecosystem for cloud-native applications"
        ], "kubernetes logo"),
        ("Why Kubernetes Matters", [
            "Enables efficient resource utilization",
            "Facilitates microservices architecture",
            "Ensures high availability and fault tolerance",
            "Supports multi-cloud and hybrid cloud deployments",
            "Accelerates development and deployment cycles"
        ], "cloud computing"),
        ("Kubernetes in the Industry", [
            "Fastest growing technology in cloud computing",
            "173% growth in job searches year-over-year",
            "Adopted by 78% of companies in production environments (CNCF Survey 2021)",
            "Supported by all major cloud providers (AWS, Azure, GCP)",
            "Critical component in DevOps and SRE practices"
        ], "tech growth chart"),
        ("Key Kubernetes Concepts", [
            "Pods: Smallest deployable units",
            "Services: Network abstraction for pod access",
            "Deployments: Declarative updates for pods and ReplicaSets",
            "Namespaces: Virtual clusters for resource isolation",
            "ConfigMaps and Secrets: Configuration management"
        ], "container technology"),
        ("Kubernetes Architecture", [
            "Control Plane: Manages the cluster state",
            "- API Server, Scheduler, Controller Manager, etcd",
            "Worker Nodes: Run containerized applications",
            "- Kubelet, Container Runtime, kube-proxy",
            "Add-ons: DNS, Dashboard, Networking, etc."
        ], "network architecture"),
        ("Kubernetes Ecosystem", [
            "Container runtimes: Docker, containerd, CRI-O",
            "Networking: Calico, Flannel, Cilium",
            "Service Mesh: Istio, Linkerd",
            "Package Management: Helm",
            "CI/CD Integration: Jenkins, GitLab, ArgoCD"
        ], "tech ecosystem")
    ]

    for title, content, image_query in intro_slides:
        add_content_slide(prs, title, content, image_query)

    # Course Content Slides
    course_slides = [
        ("Course Overview", [
            "Understanding core Kubernetes concepts",
            "Hands-on experience with cluster setup and management",
            "Deep dive into Kubernetes components and architecture",
            "Best practices for security, networking, and storage",
            "Preparation for the Certified Kubernetes Administrator exam"
        ], "online course"),
        ("Unique Course Features", [
            "Interactive coding exercises in live Kubernetes environment",
            "Browser-based practice - no high-end system required",
            "Real-world scenarios and problem-solving challenges",
            "Comprehensive coverage of CKA exam objectives"
        ], "e-learning"),
        ("60-Day Free Kubernetes Cluster", [
            "We help you create a Kubernetes cluster for training",
            "Free of cost or at minimal cost for 60 days",
            "99% under your control - not managed by us",
            "Learn at your own pace within the 60-day period",
            "Hands-on experience with a real Kubernetes environment"
        ], "server cluster"),
        ("Flexible Learning", [
            "Access to training materials for 60 days",
            "Self-paced learning - study whenever you want",
            "Practice on your personal Kubernetes cluster",
            "Combine theoretical knowledge with practical application"
        ], "flexible work")
    ]

    for title, content, image_query in course_slides:
        add_content_slide(prs, title, content, image_query)

    prs.save('Kubernetes_Course_Presentation.pptx')

if __name__ == "__main__":
    create_presentation()

```

** RUN SCRIPT **

```
python your_script_name.py
```

