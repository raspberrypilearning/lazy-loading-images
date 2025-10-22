图像的文件大小可能很大。

当网页加载时，所有图像都会被加载，这会占用大量带宽。

你可以通过仅在需要时加载图像来提高浏览器性能。 这被称为“延迟加载”。

以下是一些延迟加载图像的示例：

![一个 gif，显示图像进入浏览器视口时正在加载。](images/background-attachment-fixed.gif)

具体操作如下：

**1 - 为每个图像元素添加新属性**

在你的 HTML 文件中，为每个 `<img>` 元素添加一个 `data-src` 属性，并将属性值设置为您想要加载的图像文件。

将每个 `<img>` 元素的 `src` 属性设置为占位符图像文件（或旋转动画/gif）。

下面是一个示例：

## --- code ---

language: html
filename:
line_numbers: false
line_number_start:
line_highlights:
-----------------------------------------------------

<img src="spinner.gif" data-src="snail.svg" />

\--- /code ---

**2 - 使用交叉观察器**

创建一个 JavaScript 交叉观察器来观察每个图像元素，当图像进入视口时，将其 `src` 属性的值更改为其 `data-src` 属性的值（要加载的图像文件）。

你可以使用 JavaScript 来观察每一个 `<img>` 元素。

以下是 [更多 Web](https://projects.raspberrypi.org/en/raspberrypi/more-web) 路径中的 [动画故事](https://projects.raspberrypi.org/en/projects/animated-story) 项目中的一个示例：

## --- code ---

language: js
filename:
line_numbers: true
line_number_start: 1
line_highlights:
-----------------------------------------------------

const lazyImages = document.querySelectorAll("img");
const imageObserver = new IntersectionObserver((entries) => {
entries.forEach(
(entry) => {
if (entry.isIntersecting) {
entry.target.src = entry.target.getAttribute("data-src");
imageObserver.unobserve(entry.target);
}
}
);
});
lazyImages.forEach((lazyImage) => imageObserver.observe(lazyImage));

\--- /code ---
