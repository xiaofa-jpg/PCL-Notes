# 滤波

PCL中总结了集中需要进行点云滤波处理的情况，分别如下：
(1) 点云数据密度不规则需要平滑。
(2) 因为遮挡等问题造成离群点需要去除。
(3) 大量数据需要进行下采样。
(4) 噪声数据需要去除。

PCL中点云滤波模块提供了很多灵活实用的滤波处理算法，例如双边滤波、高斯滤波、条件滤波、直通滤波、基于随机采样一整行滤波等。

下边给出两个下采样类的应用实例。（VoxelGrid、UniformSampling）

```
#include <pcl/io/pcd_io.h>
#include <pcl/point_types.h>
// 包含相关头文件
#include <pcl/filters/voxel_grid.h>
#include <pcl/filters/uniform_sampling.h>

typedef pcl::PointXYZ PointT;

int main(int argc, char** argv)
{
	// 读取点云
	pcl::PointCloud<PointT>::Ptr cloud(new pcl::PointCloud<PointT>);
	pcl::io::loadPCDFile(argv[1], *cloud);
	std::cout << "original cloud size : " << cloud->size() << std::endl;

	// 使用体素化网格(VoxelGrid)进行下采样
	pcl::VoxelGrid<PointT> grid; //创建滤波对象
	const float leaf = 0.005f; 
	grid.setLeafSize(leaf, leaf, leaf); // 设置体素体积
	grid.setInputCloud(cloud); // 设置点云
	pcl::PointCloud<PointT>::Ptr voxelResult(new pcl::PointCloud<PointT>);
	grid.filter(*voxelResult); // 执行滤波，输出结果
	std::cout << "voxel downsample size :" << voxelResult->size() << std::endl;

	// 使用UniformSampling进行下采样
	pcl::UniformSampling<PointT> uniform_sampling;
	uniform_sampling.setInputCloud(cloud);
	double radius = 0.005f;
	uniform_sampling.setRadiusSearch(radius);
	pcl::PointCloud<PointT>::Ptr uniformResult(new pcl::PointCloud<PointT>);
	uniform_sampling.filter(*uniformResult);
	std::cout << "UniformSampling size :" << uniformResult->size() << std::endl;
	
	system("pause");
	return 0;
}
```