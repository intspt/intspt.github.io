---
layout: base
permalink: /note/2017-12-13-00
title: dismissViewControllerAnimated的一个坑
---

最近发现在UITableView的tableView:didSelectRowAtIndexPath:代理方法内调用UIViewController的dismissViewControllerAnimated:animated:有时候会延迟执行

解决办法是把这个语句放到主线程中执行

    dispatch_async(dispatch_get_main_queue(), ^{
        [self.delegate controller:self selectSectionTitle:sectionTitle Product:self.filteredBizArrays[indexPath.section][indexPath.row]];
    });

但是tableView:didSelectRowAtIndexPath:这个方法本身就是在主线程中执行的

大概是个bug吧