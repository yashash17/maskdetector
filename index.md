## Background

You can use the [editor on GitHub](https://github.com/yashash17/maskdetector/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

The COVID-19 pandemic has been one of the most deadly pandemics in the history of mankind. To date, there have been ~260 million cases worldwide resulting in ~5 million deaths and both these numbers are only expected to grow. With the emergence of new variants, even fully vaccinated individuals can contract COVID-19. This makes masks a primary resource to limit the spread of the virus. Even though mask mandates currently exist, many flout the rules and can easily get away with it. Manually checking for people wearing masks is tedious and expensive, so the development of an automated system to detect masks is of key importance. It can help save lives by establishing stricter compliance. 

### Idea

Develop a system that accurately detects the presence of a mask on multiple faces either in real-time video or static images. This approach can be used by entities ranging from restaurants to local governments to universities. For example, if you have to enter a library on campus where it is compulsory to wear masks, you will only be given permission if your scan before entering the library detects the presence of a mask. Next, while in the library, CCTV cameras can be configured to catch those that are constantly spotted without masks using facial recognition and a more sophisticated version of the model built in this project. 

### Current state-of-the-art

1. For static images:

Current algorithms first perform facial recognition and then use a sophisticated R-CNN (Convolutional Neural Network) model to detect the presence of a mask once a face is successfully detected. 

2. For real-time video streams:

The process is esentially the same with additional complexities. The algorithm first identifies multiple frames of the same person using facial recognition. It then uses a similar R-CNN model to detect the presence of masks in each frame. The resultant classification for each frame at any given time is computed as an average result of the previous immediate frames. Multiple frames reduce the possibility of false-classification if facial recognition fails due to multiple reasons (unclear video, face being too obscured etc.)

https://tryolabs.com/blog/2020/07/09/face-mask-detection-in-street-camera-video-streams-using-ai-behind-the-curtain

## Development Steps and Timeline of Project

- **November 30th**: Find dataset online and train model on the same
- **December 3rd**: Implement script to detect face-mask in static images
- **December 5th**: Test accuracy of model on real images (clicked by myself) and those that I found online
- **December 8th**: Implement script to detect face-mask in real-time video streams December 10th. Test accuracy of model on different videos
- **December 13th**: Try to find/ manipulate better datasets to improve the accuracy of the model and finalize presentation + project webpage

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/yashash17/maskdetector/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
