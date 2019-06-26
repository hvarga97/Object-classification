//#define CRT_SECURE_NO_WARNINGS_
#include "stdafx.h"
#include <iostream>
#include <fstream>

//#include <pcl/common/centroid.h>
#include <pcl/common/impl/centroid.hpp>
#include <pcl/point_types.h>
#include <pcl/io/vtk_lib_io.h>
#include <pcl/visualization/pcl_visualizer.h>
#include <pcl/visualization/common/actor_map.h>
#include <pcl/io/pcd_io.h>
#include <pcl/apps/render_views_tesselated_sphere.h>
#include <pcl/features/esf.h>

#include <opencv2/opencv.hpp>
#include <opencv2/core/core.hpp>
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui/highgui.hpp>
#include <string>



using namespace pcl;
using namespace pcl::apps;
using namespace pcl::io;
using namespace std;


using namespace cv;
int main(int argc, char** argv)
{
	char c[300];
	//string c;
	FILE *fp;
	fp = fopen("C://Users/hvarg/Desktop/modeli.txt", "r");

	std::ifstream infile("C://Users/hvarg/Desktop/modeli.txt");
	std::string file_path;
	//fgets(c, sizeof c, fp);
	FILE *fpDescriptor = fopen("descriptor.txt", "wb"); //fwrite
	fclose(fpDescriptor);

	//while (fgets(c, sizeof c, fp) != NULL)
	while (std::getline(infile, file_path))
	{
		istringstream iss(file_path);
		string filepath;
		iss >> filepath;
		if (filepath.compare("end") == 0)
			break;
		vtkSmartPointer<vtkPolyData> polydata;
		vtkSmartPointer<vtkPLYReader> reader = vtkSmartPointer<vtkPLYReader>::New();

		//reader->SetFileName("C://Users/hvarg/Desktop/Cat10_ModelDatabase/apple/3a92a256ad1e060ec048697b91f69d2.ply");
		//reader->SetFileName("C://Users/hvarg/Desktop/Cat10_ModelDatabase/banana/7d78e217e0ba160fe2b248b8bb97d290.ply");
		printf("%s\n", filepath); //??
		strcpy(c, filepath.c_str());
		reader->SetFileName(c);
		reader->Update();
		polydata = reader->GetOutput();

		float resx = 64;
		float resy = resx;

		vector<PointCloud<PointXYZ>, Eigen::aligned_allocator<PointCloud<PointXYZ> > >  views;
		vector<Eigen::Matrix4f, Eigen::aligned_allocator<Eigen::Matrix4f> > poses;
		vector<float> entropies;

		visualization::PCLVisualizer vis;
		vis.addModelFromPolyData(polydata, "mesh1", 0);
		vis.setRepresentationToSurfaceForAllActors();
		vis.renderViewTesselatedSphere(resx, resy, views, poses, entropies, 1);

		//typedef PointCloud<pcl::PointXYZ>::Ptr CloudPtr;
		//RenderViewsTesselatedSphere render_views;
		//render_views.addModelFromPolyData(polydata);
		//render_views.setResolution(64);
		//render_views.setTesselationLevel(1); //80 views
		//render_views.addModelFromPolyData(polydata); //vtk model
		//render_views.setGenOrganized(false);
		//render_views.generateViews();
		//vector< CloudPtr > views;
		//render_views.getViews(views);
		//render_views.getPoses(poses);


		PointCloud<PointXYZ>::Ptr object(new PointCloud<PointXYZ>);

		PointCloud<ESFSignature640>::Ptr descriptor(new PointCloud<ESFSignature640>);

		//while (!vis.wasStopped())
		//{
		//}

		//FILE *fpPCD = fopen("views.pcd", "w");

		PointCloud<PointXYZ> cloud;
		cloud.width = views.size();

		cloud.is_dense = false;
		ESFEstimation<PointXYZ, ESFSignature640> esf;


		for (int i = 0; i < views.size(); i++)
		{
			for (int j = 0; j < views[i].size(); j++)
			{
				cloud.height = views[i].size();
				cloud.points.resize(cloud.width * cloud.height);
				cloud.points[j].x = views[i][j].x;
				cloud.points[j].y = views[i][j].y;
				cloud.points[j].z = views[i][j].z;


				//fprintf(fpPCD, "%f\t%f\t%f\t\n", views_xyz[i][j].x, views_xyz[i][j].y, views_xyz[i][j].z);
			}

			//for (int i = 0; i < views.size(); i++)
			//{
			//	for (int j = 0; j < views[i]->size(); j++)
			//	{
			//		cloud.height = views[i]->size();
			//		cloud.points.resize(cloud.width * cloud.height);
			//		cloud.points[j].x = views[i]->at(j).x;
			//		cloud.points[j].y = views[i]->at(j).y;
			//		cloud.points[j].z = views[i]->at(j).z;
			//	}


			savePCDFileASCII("test_pcd.pcd", cloud);

			// Read a PCD file from disk.
			if (loadPCDFile<PointXYZ>("test_pcd.pcd", *object) != 0)
			{
				return -1;
			}

			// ESF estimation object.
			esf.setInputCloud(object);

			esf.compute(*descriptor);


			fpDescriptor = fopen("descriptor.txt", "ab"); //fwrite
			for (int k = 0; k < descriptor->size(); k++)
			{
				for (int l = 0; l < descriptor->at(k).descriptorSize(); l++)
				{
					double h = descriptor->at(k).histogram[l];
					fwrite(&h, 1, sizeof(h), fpDescriptor);
					//fprintf(fpDescriptor, "%.5f\n", h);
				}
			}
			fclose(fpDescriptor);
		}
		//fclose(fpPCD);
	}


	fclose(fp);








	
	
	//if (image.empty())                      // Check for invalid input
	//{
	//	cout << "Could not open or find the image" << std::endl;
	//	return -1;
	//}
	//namedWindow("Display window", WINDOW_AUTOSIZE); // Create a window for display.
	//imshow("Display window", image);                // Show our image inside it.
	//waitKey(0); // Wait for a keystroke in the window
	
	
	//FILE *fpPCD = fopen("oblak.txt", "w");

	char c[300];
	FILE *fp;
	fp = fopen("C://Users/hvarg/Desktop/scene.txt", "r");
	ifstream infile("C://Users/hvarg/Desktop/scene.txt");
	ifstream infile_png("C://Users/hvarg/Desktop/scene_png.txt");
	string file_path, file_path_png;
	FILE *Descriptor_scene_2 = fopen("descriptor_scene.txt", "wb"); //fwrite
	fclose(Descriptor_scene_2);
	while (std::getline(infile, file_path) && std::getline(infile_png, file_path_png))
	{
		istringstream iss_png(file_path_png);
		string filepath_png;
		iss_png >> filepath_png;
		if (filepath_png.compare("end") == 0)
			break;


		//String imageName("C:/Users/hvarg/Desktop/segmentirane slike/tt_bnn_veg26.objmap.png"); // by default
		Mat image;
		image = imread(filepath_png); // Read the file
		cvtColor(image, image, COLOR_BGR2GRAY);

		istringstream iss(file_path);
		string filepath;
		iss >> filepath;
		if (filepath.compare("end") == 0)
			break;

		//ucitaj depth sliku
		PointCloud<PointXYZ> oblak;
		oblak.width = image.rows;
		oblak.height = image.cols;
		oblak.is_dense = false;
		PointCloud<PointXYZ>::Ptr objekt(new PointCloud<PointXYZ>);
		strcpy(c, filepath.c_str());
		loadPCDFile<PointXYZ>(c, *objekt);
		int br255 = 0, br = 0;
		for (int rows = 0; rows < image.rows; rows++)
			for (int cols = 0; cols < image.cols; cols++)
				if (image.at<uchar>(rows, cols) == 255)
				{
					//oblak.points.resize(oblak.width * oblak.height);
					//oblak.points[br].x = objekt->at(rows*image.rows+cols).x;
					//oblak.points[br].y = objekt->at(rows*image.rows+cols).y;
					//oblak.points[br].z = objekt->at(rows*image.rows+cols).z;
					//
					//fprintf(fpPCD, "%f\t%f\t%f\t\n", oblak.points[br].x, oblak.points[br].y, oblak.points[br].z);
					br255++;
				}
		//printf("%d\n", br255);
		for (int rows = 0; rows < image.rows; rows++)
			for (int cols = 0; cols < image.cols; cols++)
				if (image.at<uchar>(rows, cols) == 255)
				{
					oblak.points.resize(oblak.width*oblak.height);
					oblak.points[br].x = objekt->at(rows*image.rows + cols).x;
					oblak.points[br].y = objekt->at(rows*image.rows + cols).y;
					oblak.points[br].z = objekt->at(rows*image.rows + cols).z;

					//fprintf(fpPCD, "%f\t%f\t%f\t\n", oblak.points[br].x, oblak.points[br].y, oblak.points[br].z);
					br++;
				}
		//scale to unit sphere
		/*CentroidPoint<pcl::PointXYZ> centroid;
		centroid.add(oblak.points.);
		pcl::PointXYZ c1;
		centroid.get(c1);*/

		//int broj = 0;
		long double najveci = 0;
		Eigen::Vector4f centroid;
		compute3DCentroid(oblak, centroid);
		for (int broj = 0; broj < oblak.points.size(); broj++)
		{
			long double udaljenost = sqrt(pow(oblak.points[broj].x - centroid(0), 2.0) + pow(oblak.points[broj].y - centroid(1), 2.0) + pow(oblak.points[broj].z - centroid(2), 2.0));
			if (udaljenost >= najveci)
				najveci = udaljenost;
			//broj++;
		}

		//printf("%f\n%f\n%f\n", centroid(0), centroid(1), centroid(2));

		int br1 = 0;
		for (int br1 = 0; br1 < oblak.points.size(); br1++)
		{
			oblak.points[br1].x = oblak.points[br1].x / najveci;
			oblak.points[br1].y = oblak.points[br1].y / najveci;
			oblak.points[br1].z = oblak.points[br1].z / najveci;
		}



		savePCDFileASCII("oblak_pcd.pcd", oblak);
		//fclose(fpPCD);


		PointCloud<PointXYZ>::Ptr objekt_a(new PointCloud<PointXYZ>);
		ESFEstimation<PointXYZ, ESFSignature640> esff;
		PointCloud<ESFSignature640>::Ptr deskriptor(new PointCloud<ESFSignature640>);

		// Read a PCD file from disk.
		if (loadPCDFile<PointXYZ>("oblak_pcd.pcd", *objekt_a) != 0)
		{
			return -1;
		}

		// ESF estimation object.
		esff.setInputCloud(objekt_a);

		esff.compute(*deskriptor);
		FILE *Deskriptor_scene_2 = fopen("descriptor_scene.txt", "ab"); //fwrite
		for (int brojac = 0; brojac < deskriptor->size(); brojac++)
		{
			for (int brojac1 = 0; brojac1 < deskriptor->at(brojac).descriptorSize(); brojac1++)
			{
				double h2 = deskriptor->at(brojac).histogram[brojac1];
				//printf("%lf\n", h2);
				fwrite(&h2, 1, sizeof(h2), Deskriptor_scene_2);
				//fprintf(fpDescriptor, "%.5f\n", h);
			}
		}
		fclose(Descriptor_scene_2);
	}
	
	return (0);
}
