# 使用TaskPool执行多个耗时任务

如果有多个任务同时执行，由于任务的复杂度不同，执行时间会不一样，返回数据的时间也是不可控的。如果宿主线程需要所有任务执行完毕的数据，那么可以通过下面这种方式实现。

除此以外，如果需要处理的数据量较大（比如一个列表中有10000条数据），把这些数据都放在一个Task中处理也是比较耗时的。那么就可以将原始数据拆分成多个列表，并将每个子列表分配给一个独立的Task进行执行，并且等待全部执行完毕后拼成完整的数据，这样可以节省处理时间，提升用户体验。

下面以多个任务进行图片加载为例进行说明。

1. 实现子线程需要执行的任务。

   ```ts
   // IconItemSource.ets
   export class IconItemSource {
     image: string | Resource = '';
     text: string | Resource = '';
   
     constructor(image: string | Resource = '', text: string | Resource = '') {
       this.image = image;
       this.text = text;
     }
   }
   ```

   ```ts
   // IndependentTask.ets
   import { IconItemSource } from './IconItemSource';
    
   // 在Task中执行的方法，需要添加@Concurrent注解，否则无法正常调用。
   @Concurrent
   export function loadPicture(count: number): IconItemSource[] {
     let iconItemSourceList: IconItemSource[] = [];
     // 遍历添加6*count个IconItem的数据
     for (let index = 0; index < count; index++) {
       const numStart: number = index * 6;
       // 此处循环使用6张图片资源
       iconItemSourceList.push(new IconItemSource('$media:startIcon', `item${numStart + 1}`));
       iconItemSourceList.push(new IconItemSource('$media:background', `item${numStart + 2}`));
       iconItemSourceList.push(new IconItemSource('$media:foreground', `item${numStart + 3}`));
       iconItemSourceList.push(new IconItemSource('$media:startIcon', `item${numStart + 4}`));
       iconItemSourceList.push(new IconItemSource('$media:background', `item${numStart + 5}`));
       iconItemSourceList.push(new IconItemSource('$media:foreground', `item${numStart + 6}`));
   
     }
     return iconItemSourceList;
   }
   ```

2. 将需要执行的Task放到了一个TaskGroup里面，当TaskGroup中所有的Task都执行完毕后，会把每个Task运行的结果都放在一个数组中返回到宿主线程，而不是每执行完一个Task就返回一次，这样就可以在返回的数据里拿到所有的Task执行结果，方便宿主线程使用。

   ```ts
   // MultiTask.ets
   import { taskpool } from '@kit.ArkTS';
   import { IconItemSource } from './IconItemSource';
   import { loadPicture } from './IndependentTask';
    
   let iconItemSourceList: IconItemSource[][];
    
   let taskGroup: taskpool.TaskGroup = new taskpool.TaskGroup();
   taskGroup.addTask(new taskpool.Task(loadPicture, 30));
   taskGroup.addTask(new taskpool.Task(loadPicture, 20));
   taskGroup.addTask(new taskpool.Task(loadPicture, 10));
   taskpool.execute(taskGroup).then((ret: object) => {
     let tmpLength = (ret as IconItemSource[][]).length
     for (let i = 0; i < tmpLength; i++) {
       for (let j = 0; j < ret[i].length; j++) {
         iconItemSourceList.push(ret[i][j]);
       }
     }
   })
   ```
