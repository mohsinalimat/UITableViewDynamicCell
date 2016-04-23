# UITableViewDynamicCell
Simple to add "Pull to refresh" and "Load more" into your UITableView

## Installation
* via werfe: github "werfe/UITableViewDynamicCell"
* or copy UITableViewDynamicCell folder to your project

## Usage
* **Import UITableView+DynamicCell category to your table**
```
#import "UITableView+DynamicCell.h"
```
* **In "viewDidAppear"**
```
-(void)viewDidAppear:(BOOL)animated{
[super viewDidAppear:animated];
_tableView.refreshDelegate = self;
_tableView.enabledLoadMore = YES;
_tableView.enabledRefresh = YES;
}
```
* **Add some methods required**
```
-(void)scrollViewDidScroll:(UIScrollView *)scrollView{
[_tableView scrollViewDidScroll:scrollView];
}
- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate
{
[self.tableView checkToReload];
}


-(void)refreshData:(UITableView *)tableView completion:(RefreshCompletion)completion{

//TODO:do some task needs many time to finish. After finish it, call the completion block

//Some codes below is an example
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(2 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
[_tableView reloadData];
completion();
});
}

-(void)loadMoreData:(UITableView *)tableView completion:(RefreshCompletion)completion{

//TODO:do some task needs many time to finish. After finish it, call the completion block

//Some codes below is an example
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(2 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
[_tableView reloadData];
completion();
});
}

```

* **That's it!**
