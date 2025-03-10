# 广度优先遍历
广度优先遍历(Breadth First Search)，又称为广度优先搜索，简称BFS。

## 1、BFS算法
如果说图的深度优先遍历类似树的前序遍历，那么图的广度优先遍历就类似于树的层序遍历了。
广度优先搜索是一种分层的查找过程，每向前走一步可能访问一批顶点，不像深度优先搜索那样有往回退的情况，因此它不是一个递归的算法。为了实现逐层的访问，算法必须借助一个辅助队列，以记忆正在访问的顶点的下一层顶点。
以下是广度优先遍历的代码：

```
/*邻接矩阵的广度遍历算法*/
void BFSTraverse(MGraph G){
	int i, j;
	Queue Q;
	for(i = 0; i<G,numVertexes; i++){
		visited[i] = FALSE;
	}
	InitQueue(&Q);	//初始化一辅助用的队列
	for(i=0; i<G.numVertexes; i++){
		//若是未访问过就处理
		if(!visited[i]){
			vivited[i] = TRUE;	//设置当前访问过
			visit(i);	//访问顶点
			EnQueue(&Q, i);	//将此顶点入队列
			//若当前队列不为空
			while(!QueueEmpty(Q)){
				DeQueue(&Q, &i);	//顶点i出队列
				//FirstNeighbor(G,v):求图G中顶点v的第一个邻接点，若有则返回顶点号，否则返回-1。
				//NextNeighbor(G,v,w):假设图G中顶点w是顶点v的一个邻接点，返回除w外顶点v
				for(j=FirstNeighbor(G, i); j>=0; j=NextNeighbor(G, i, j)){
					//检验i的所有邻接点
					if(!visited[j]){
						visit(j);	//访问顶点j
						visited[j] = TRUE;	//访问标记
						EnQueue(Q, j);	//顶点j入队列
					}
				}
			}
		}
	}
}
```
以下面这个无向图为例

![输入图片说明](https://cdn.jsdelivr.net/gh/Dec-lxh/Images@main/img/20250310105001.png)

其广度优先遍历的结果为a b c d e f g h 

## 2、BFS算法性能分析
无论是邻接表还是邻接矩阵的存储方式，BFS 算法都需要借助一个辅助队列Q, n个顶点均需入队一次，在最坏的情况下，空间复杂度为O(V)。
采用邻接表存储方式时，每个顶点均需搜索一次(或入队一次)， 在搜索任一顶点的邻接点时，每条边至少访问一次，算法总的时间复杂度为O(V + E)。采用邻接矩阵存储方式时，查找每个顶点的邻接点所需的时间为O(V)，故算法总的时间复杂度为O(V^2)

注意：图的邻接矩阵表示是唯一的，但对于邻接表来说，若边的输入次序不同，生成的邻接表也不同。因此，对于同样一个图，基于邻接矩阵的遍历所得到的DFS序列和BFS序列是唯一的，基于邻接表的遍历所得到的DFS序列和BFS序列是不唯一的。
