# 插入图片，图片下拉变大
## 插入图片的简易实现
项目搭建UI的时候，有时我们会遇到再tableView中插入一张图片，下拉的时候显示这张图片，但是上拉的时候要显示原来的tableView的背景。<br>
代码实现：<br>
```Objc
// 定义
@property (nonatomic, strong) UIImageView *imgView;
```
```Objc
// 配置背景图
[self.baseTableView addSubview:self.imgView];
[self.baseTableView sendSubviewToBack:self.imgView];
```
```Objc
// 懒加载
- (UIImageView *)imgView
{
    if (!_imgView) {
        _imgView = [[UIImageView alloc] init];
        _imgView.frame = CGRectMake(0, -kScreenHeight, kScreenWidth, kScreenHeight);
        _imgView.backgroundColor = k298CFFColor;
        _imgView.contentMode = UIViewContentModeScaleAspectFill;
        _imgView.clipsToBounds = YES;
    }
    return _imgView;
}
```
## 图片下拉变大的简易实现
```Objc
#define IMAGE_HEIGHT (图片高度)
// 定义
@property (nonatomic, strong) UIView *headerV;
```
```Objc
// 初始化
[self.tableView addSubview:self.headerV];
self.tableView.contentInset = UIEdgeInsetsMake(IMAGE_HEIGHT, 0, 0, 0);
```
```Objc
// scrollView方法
- (void)scrollViewDidScroll:(UIScrollView *)scrollView
{
    // 改变图片框的大小 (上滑的时候不改变)
    // 这里不能使用offsetY，因为当（offsetY < LIMIT_OFFSET_Y）的时候，y = LIMIT_OFFSET_Y 不等于 offsetY
    CGFloat newOffsetY = scrollView.contentOffset.y;
    
    if (newOffsetY <= -IMAGE_HEIGHT) {
        self.headerV.frame = CGRectMake(0, newOffsetY, kScreenWidth, -newOffsetY);
    }
    
//    // 禁止上拉
//    CGPoint offset = self.tableView.contentOffset;
//    if (offset.y > -IMAGE_HEIGHT) {
//        offset.y = -IMAGE_HEIGHT;
//        self.tableView.contentOffset = offset;
//    }
}
```
```Objc
// 懒加载
#pragma mark - NSObject
- (UIView *)headerV
{
    if (!_headerV) {
        _headerV = [[UIView alloc] init];
        _headerV.frame = CGRectMake(0, -IMAGE_HEIGHT, kScreenWidth, IMAGE_HEIGHT);
        _headerV.bgIV.contentMode = UIViewContentModeScaleAspectFill;
        _headerV.bgIV.clipsToBounds = YES;
}
```
