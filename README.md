# JSONKit-NSJSONSerialization-
普遍认为效率不错的JSONKit，与苹果官方的JSONSerialization究竟差距有多大？？？？
##JSONKit
![enter image description here](https://github.com/lsqiang/JSONKit-NSJSONSerialization-/blob/master/1.png?raw=true)

##NSSerialization
![enter image description here](https://github.com/lsqiang/JSONKit-NSJSONSerialization-/blob/master/2.png?raw=true)


##效率比较代码（执行100*1000次查看内存消耗）

>  - (void)loadJSONKit {
>     
>     NSString *path = [[NSBundle mainBundle] pathForResource:@"videos.json" ofType:nil];
>     
>     
>     NSURL *url = [NSURL fileURLWithPath:path];
>     
>     NSURLRequest *request = [NSURLRequest requestWithURL:url];
>     
>     [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue]completionHandler:^(NSURLResponse
> *response, NSData *data, NSError *connectionError) {
>         
>         CFAbsoluteTime start = CFAbsoluteTimeGetCurrent();
>         for (int i=0; i<100*1000; i++) {
>             [[JSONDecoder decoder] objectWithData:data];
>         }
>         NSLog(@"JSONKit耗时=====>%f", CFAbsoluteTimeGetCurrent() - start);
>     }]; }
> 
> - (void)loadJSONSerialization {
>     
>     NSString *path = [[NSBundle mainBundle] pathForResource:@"videos.json" ofType:nil];
>     
>     
>     NSURL *url = [NSURL fileURLWithPath:path];
>     
>     NSURLRequest *request = [NSURLRequest requestWithURL:url];
>     
>     [NSURLConnection sendAsynchronousRequest:request queue:[NSOperationQueue mainQueue]completionHandler:^(NSURLResponse
> *response, NSData *data, NSError *connectionError) {
>         
>         CFAbsoluteTime start = CFAbsoluteTimeGetCurrent();
>         for (int i=0; i<100*1000; i++) {
>             [NSJSONSerialization JSONObjectWithData:data options:0 error:NULL];
>         }
>         NSLog(@"NSJSONSerialization耗时=====>%f", CFAbsoluteTimeGetCurrent() - start);
>     }]; }


