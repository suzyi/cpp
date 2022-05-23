###
+ [0-installation](0-installation.md): install opencv, and deploy it on Visual Studio 2019 and then run a simple example called "bgr2gray".
+ [1-object-detection](1-object-detection): Detect objects on images with pure background.
### cv::Mat
+ `cv::hconcat(img_true, img_recon, img_concat);`
+ `cv::imwrite("result/1.png", img_concat);`
+ `cv::Mat img(int rows, int cols, int type);`
  + `img.at<float>(i, j) = 2*CV_PI*rng.uniform(0.0, 1.0);` i-th row, j-th col.
+ `cv::Mat img = cv::imread("data/1.png", -1);`
  + `-1` unchanged, `0` grayscale.
  + `cv_img.create(height, width, CV_8UC(channels));`
  + `cv_img.size()` will print (width, height).
  + `cv_img.channels()`
  + `cv_img.type()`
  + `cv_img.reshape(int cn, int rows)`
    + `cn` specifies channels.
  + `cv_img.t()` transpose.
+ `double minVal; double maxVal; cv::minMaxLoc(img_float, &minVal, &maxVal); std::cout << "min val: " << minVal << std::endl;`
+ `cv::Mat(kernel_gradients, cv::Rect(top_left_x, top_left_y, kernel_size.width, kernel_size.height));`
+ `cv::repeat(InputArray src, int ny, int nx, OutputArray dst);`
  + `ny` Flag to specify how many times the `src` is repeated along the vertical axis.
  + `nx` how many times along horizontal axis.
+ `cv::resize(img, img_resized, net_in_height_width);`
  + `cv::Mat img_float; img_resized.convertTo(img_float, CV_32FC3);` or `img_resized.convertTo(img_float, CV_32FC3);`
+ `std::vector<cv::Mat> input_channels; cv::split(img_float, input_channels);`
+ `cv::Size kernel_size(16, 8);`
  + `kernel_size.width` prints 16, `kernel_size.height` prints 8.
+ `int s = cv::sum(img_resized)[0];`