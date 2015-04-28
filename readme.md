st__author__ = 'kby'
File = open("/home/kby/Downloads/testset.txt")
line = File.readline()
x = []
y = []
h = []
print line
while line:
    line = line.strip().split(",")
    x.append(float(line[0]))
    y.append(float(line[1]))
    h.append(float(line[2]))
    line = File.readline()
File.close()
print x
print y
print h
n = len(h)
x1 = [0 for i in range(n)]
y1 = [0 for i in range(n)]
h1 = [0 for i in range(n)]
m = [0 for i in range(n)]
j = [0 for i in range(n)]
J = 0.0
J1 = 0.0
epsilon = 0.0000001
ap = 0.001
theta0, theta1, theta2 = 1.0, 1.0, 1.0
tem1, tem2, tem3 = 0.0, 0.0, 0.0
for i in range(n):
    max1, max2, max3, min1, min2, min3 = max(x), max(y), max(h), min(x), min(y), min(h)
    x1[i] = (x[i]-min1)/(max1-min1)
    y1[i] = (y[i]-min2)/(max2-min2)
    h1[i] = (h[i]-min3)/(max3-min3)
    print x1, y1, h1
while True:
    for i in range(n):
        m[i] = (theta0*x1[i]+theta1*y1[i]+theta2)
        j[i] = (m[i]-h1[i])
        tem1 -= (ap * j[i] * x1[i]) / n
        tem2 -= (ap * j[i] * y1[i]) / n
        tem3 -= (ap * j[i] * 1) / n
    theta0 += tem1
    theta1 += tem2
    theta2 += tem3
    for i in range(n):
        m[i] = (theta0*x1[i]+theta1*y1[i]+theta2)
        j[i] = (m[i]-y1[i])
        J += (j[i]*j[i])/(2*n)
        print theta0,theta1,theta2,J
    if ((J-J1)**2) < epsilon:
        break
    else:
        J1 = J
        J = 0.0
for i in range(n):
        m[i] = (theta0*x1[i]+theta1*y1[i]+theta2)*521000
print m
print x
print y
print h

