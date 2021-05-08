# UTS-PengolahCitraa

berikut hasilnya

![sn](https://user-images.githubusercontent.com/81818405/117519639-8e45e080-afce-11eb-8813-22e7baca821d.PNG)

berikut sourceCodenya

function varargout = Guide(varargin)
% GUIDE MATLAB code for Guide.fig
%      GUIDE, by itself, creates a new GUIDE or raises the existing
%      singleton*.
%
%      H = GUIDE returns the handle to a new GUIDE or the handle to
%      the existing singleton*.
%
%      GUIDE('CALLBACK',hObject,eventData,handles,...) calls the local
%      function named CALLBACK in GUIDE.M with the given input arguments.
%
%      GUIDE('Property','Value',...) creates a new GUIDE or raises the
%      existing singleton*.  Starting from the left, property value pairs are
%      applied to the GUI before Guide_OpeningFcn gets called.  An
%      unrecognized property name or invalid value makes property application
%      stop.  All inputs are passed to Guide_OpeningFcn via varargin.
%
%      *See GUI Options on GUIDE's Tools menu.  Choose "GUI allows only one
%      instance to run (singleton)".
%
% See also: GUIDE, GUIDATA, GUIHANDLES

% Edit the above text to modify the response to help Guide

% Last Modified by GUIDE v2.5 06-May-2021 23:35:59

% Begin initialization code - DO NOT EDIT
gui_Singleton = 1;
gui_State = struct('gui_Name',       mfilename, ...
                   'gui_Singleton',  gui_Singleton, ...
                   'gui_OpeningFcn', @Guide_OpeningFcn, ...
                   'gui_OutputFcn',  @Guide_OutputFcn, ...
                   'gui_LayoutFcn',  [] , ...
                   'gui_Callback',   []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end

if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end
% End initialization code - DO NOT EDIT


% --- Executes just before Guide is made visible.
function Guide_OpeningFcn(hObject, eventdata, handles, varargin)

handles.output = hObject;

guidata(hObject, handles);

%buat axes
ah = axes('unit', 'normalized', 'position', [0 0 1 1]);
% import background
bg = imread('gam.jfif'); imagesc(bg);
% matikan axes dan tampilkan background
set(ah,'handlevisibility','off','visible','off')

% --- Outputs from this function are returned to the command line.
function varargout = Guide_OutputFcn(hObject, eventdata, handles) 
% varargout  cell array for returning output args (see VARARGOUT);
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Get default command line output from handles structure
varargout{1} = handles.output;


% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

[filename,pathname] = uigetfile({'*.jpg','*.png'});
if ~isequal(filename,pathname,0)
    Img=imread(fullfile(pathname,filename));
    axes(handles.axes1);
    imshow(Img);
    title('Gambar Asli');
    R = Img(:,:,1);
    G = Img(:,:,2);
    B = Img(:,:,3);
else
    return
end
handles.Img=Img;
handles.R=R;
handles.G=G;
handles.B=B;
guidata(hObject,handles)

% --- Executes on button press in radiobutton1.
function radiobutton1_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hint: get(hObject,'Value') returns toggle state of radiobutton1
set(hObject,'Value',1)
set(handles.radiobutton2,'Value',0)
set(handles.radiobutton3,'Value',0)
set(handles.radiobutton4,'Value',0)
set(handles.radiobutton5,'Value',0)
set(handles.radiobutton6,'Value',0)

Img=handles.Img;
R=handles.R;
G=handles.G;
B=handles.B;
axes(handles.axes2)
imshow(Img)
title('Citra RGB')
axes(handles.axes3)
h=histogram(R,256);
h.FaceColor='r';
h.EdgeColor='r';

xlim([0,225])
grid on
hold on
h=histogram(G,256);
h.FaceColor='g';
h.EdgeColor='g';
xlim([0,225])
grid on
h=histogram(B,256);
h.FaceColor='b';
h.EdgeColor='b';
xlim([0,225])
grid on
hold off
title('Histogram')

% --- Executes on button press in radiobutton2.
function radiobutton2_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hint: get(hObject,'Value') returns toggle state of radiobutton2
set(hObject,'Value',1)
set(handles.radiobutton1,'Value',0)
set(handles.radiobutton3,'Value',0)
set(handles.radiobutton4,'Value',0)
set(handles.radiobutton5,'Value',0)
set(handles.radiobutton6,'Value',0)

R=handles.R;
G=handles.G;
B=handles.B;
axes(handles.axes2)
Red=cat(3,R,G*0,B*0);
imshow(Red)
title('Citra RED')
axes(handles.axes3)
h=histogram(R,256);
h.FaceColor='r';
h.EdgeColor='r';
xlim([0,255])
grid on
title('Histogram')

% --- Executes on button press in radiobutton4.
function radiobutton3_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hint: get(hObject,'Value') returns toggle state of radiobutton3
set(hObject,'Value',1)
set(handles.radiobutton1,'Value',0)
set(handles.radiobutton2,'Value',0)
set(handles.radiobutton4,'Value',0)
set(handles.radiobutton5,'Value',0)
set(handles.radiobutton6,'Value',0)

R=handles.R;
G=handles.G;
B=handles.B;
axes(handles.axes2)
Green=cat(3,R*0,G,B*0);
imshow(Green)
title('Citra GREEN')
axes(handles.axes3)
h=histogram(G,256);
h.FaceColor='g';
h.EdgeColor='g';
xlim([0,255])
grid on
title('Histogram')

% --- Executes on button press in radiobutton4.
function radiobutton4_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton4 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hint: get(hObject,'Value') returns toggle state of radiobutton4
set(hObject,'Value',1)
set(handles.radiobutton1,'Value',0)
set(handles.radiobutton2,'Value',0)
set(handles.radiobutton3,'Value',0)
set(handles.radiobutton5,'Value',0)
set(handles.radiobutton6,'Value',0)

R=handles.R;
G=handles.G;
B=handles.B;
axes(handles.axes2)
Blue=cat(3,R*0,G*0,B);
imshow(Blue)
title('Citra BLUE')
axes(handles.axes3)
h=histogram(B,256);
h.FaceColor='b';
h.EdgeColor='b';
xlim([0,255])
grid on
title('Histogram')

% --- Executes on button press in radiobutton5.
function radiobutton5_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton5 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hint: get(hObject,'Value') returns toggle state of radiobutton5
set(hObject,'Value',1)
set(handles.radiobutton1,'Value',0)
set(handles.radiobutton2,'Value',0)
set(handles.radiobutton3,'Value',0)
set(handles.radiobutton4,'Value',0)
set(handles.radiobutton6,'Value',0)

Img=handles.Img;
Gray=rgb2gray(Img);

axes(handles.axes2)
imshow(Gray)
title('Citra GRAYSCALE')

axes(handles.axes3)
h=histogram(Gray,256);
h.FaceColor=[.5 .5 .5];
h.EdgeColor=[.5 .5 .5];
xlim([0,255])
grid on
title('Histogram')


% --- Executes on button press in radiobutton6.
function radiobutton6_Callback(hObject, eventdata, handles)
% hObject    handle to radiobutton6 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hint: get(hObject,'Value') returns toggle state of radiobutton6
set(hObject,'Value',1)
set(handles.radiobutton1,'Value',0)
set(handles.radiobutton2,'Value',0)
set(handles.radiobutton3,'Value',0)
set(handles.radiobutton4,'Value',0)
set(handles.radiobutton5,'Value',0)

Img=handles.Img;
Gray=rgb2gray(Img);
Imgbw=im2bw(Gray);

axes(handles.axes2)
imshow(Imgbw)
title('Citra BINER')

axes(handles.axes3)
h=histogram(double(Imgbw(:)),2);
h.FaceColor= [0 0 0];
h.EdgeColor= [0 0 0];
set(gca,'Xlim',[0 1])
grid on
title('Histogram')
