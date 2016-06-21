Read me file for 3D ray tracer

Code operates such that the points of a ray or ray bundle are stored in a list and this list is plotted.
A ray or ray bundle is defined and propagating them through the lens or sphere adds a point to the ray class at intersection and changes the direction of the ray.
By propagating the ray or ray bundle through both classes all vertices of the ray have been added as points in the ray.

Ray class:

initialisation: input starting position vector for ray: (x,y,z)
		input starting direction vector for ray: (i,j,k)
		Both starting points and directions are added to: position list: self.plist, direction list: self.klist, respectively

define ray example:
ray=Ray(0.0,0.0,0.0,1.0,1.0,1.0)
ray passing through origin at x=y=z

append: adds new ray position (x1,y1,z1) and direction (i1,j1,k1) to self.plist and self.klist respectively

pp: returns last point on self.plist

kk: returns last direction on self.klist

plot: plots ray in the y-z axis by making the list of points into a matrix and setting the co-ordinate axis as appropriate columns in the matrix.


SphericalRefraction class:

initialisation: input intersection between surface and z axis: z0
		input curvature which is 1/(radius of spherical lens): curvature
		input refractive indices of first and second material the ray passes through: n1, n2
		input aperture radius of sphere: apertureradius
		if curvature is not 0: centre of lens is defined as self.O: z0+the radius
		if curvature is 0: spherical lens becomes a plane and normal to the plane is defined as the direction vector (0.0,0.0,1.0)
		when initialising sphere with curvature 0 the curvature must be inputted as an integer

intercept: if curvature is 0 this returns the intercept between the ray and the plane by using equations for when a line intersects a plane
	   if curvature is not zero this returns intercept between the sphere and the ray by using vector algebra.
	   The first value for the intercept is always taken using the if condition where the smaller intercept is always returned

refractedray: changes direction of ray by using snell's law of refraction
	      if curvature is 0 normal to the plane is perpendicular to z axis
	      if curvature is not 0 normal to the surface of the intersection point is the direction vector of the radius
	      total internal reflection is considered by using if condition where if it occurs the function returns nothing

propagate ray: adds both the intercept return to the list of positions in the ray class and refractedray return to list of directions

propagate_raybundle: implements propagate_ray function for every element in raybundle list

in order to propagate a ray through this class one must first define a ray and use it in the function:
ray=Ray(0.0,0.0,0.0,1.0,1.0,1.0)
sphere=SphericalRefraction(100.0,0.03,1.0,1.5,300)
sphere.propagate_ray(ray)

OutputPlane class:

initialisation: input point on plane (a,b,c) and direction of plane (d,e,f)

interceptplane: returns point of intersection between ray and plane

propagate_ray: adds the interceptplane function to the list of positions in the Ray class

this class can be used the same way as the SphericalRefraction class

RayBundle class:

initialisation: input R as a list of the different radii
		input N as the number of rays for the respective radius in list R
		input starting point: (m1,m2,m3)
		input direction: (n1,n2,n3)
		for loop generates parallel rays using Ray class parameters and creates a bundle with set radii R

plot: plots raybundle in y,z plane
      for loop defines each ray in the bundle as a matrix with co-ordinate axis defined as the columns of the matrix

xyplane: plots raybundle in xy plane

RMStotal: calculates root mean square value of the spacing between points in the x-y plane plots

To propagate ray bundle through sphere and plane one must first define R, N, RayBundle, SphericalRefraction, OutputPlane and use propagate_raybundle functions.
example:
R=[1.0,2.0,3.0]
N=[10,20,30]
rb=raytracer.RayBundle(R,N,0.0,0.0,0.0,0.0,0.0,1.0)
sp=raytracer.SphericalRefraction(100.0,0.03,1.0,1.5,300.0)
op=raytracer.OutputPlane(0.0,0.0,500.0,0.0,0.0,1.0)
sp.propagate_raybundle(rb)
op.propagate_raybundle(rb)