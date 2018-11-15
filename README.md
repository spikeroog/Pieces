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
        _imgView.frame = CGRectMake(0, -kScreenHeight, kScreenWith, kScreenHeight);
        _imgView.backgroundColor = k298CFFColor;
        _imgView.contentMode = UIViewContentModeScaleAspectFill;
        _imgView.clipsToBounds = YES;
    }
    return _imgView;
}
```
