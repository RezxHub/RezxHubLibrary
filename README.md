
local maincolor = Color3.fromRGB(25, 25, 25)
local firstpage = '' 
local old = game.CoreGui:FindFirstChild('ScreenGui') 
if old  then 
	old:Destroy()
end
local function Vector2ToUDim2(v2)
	return UDim2.new(0, v2.X, 0, v2.Y)
end
local tween = game:GetService("TweenService")
local library = {currenttab = '',toggled = false}
local RainbowModeColorValue = 0
coroutine.wrap(function()
	while wait() do
		RainbowModeColorValue = RainbowModeColorValue + 1 / 255
		if RainbowModeColorValue >= 1 then
			RainbowModeColorValue = 0
		end
	end
end)()

local function dragify(Frame)
	dragToggle = nil
	dragSpeed = 2 
	dragInput = nil
	dragStart = nil
	dragPos = nil
	function updateInput(input)
		if not busy  then 
			Delta = input.Position - dragStart
			Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + Delta.X, startPos.Y.Scale, startPos.Y.Offset + Delta.Y)
			game:GetService("TweenService"):Create(Frame, TweenInfo.new(.25), {Position = Position}):Play()
		end 
	end
	Frame.InputBegan:Connect(function(input)
		if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
			dragToggle = true
			dragStart = input.Position
			startPos = Frame.Position
			input.Changed:Connect(function()
				if (input.UserInputState == Enum.UserInputState.End) then
					dragToggle = false
				end
			end)
		end
	end)
	Frame.InputChanged:Connect(function(input)
		if (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
			dragInput = input
		end
	end)
	game:GetService("UserInputService").InputChanged:Connect(function(input)
		if (input == dragInput and dragToggle) then
			updateInput(input)
		end
	end)
end
local ScreenGui = Instance.new("ScreenGui")
local bind = Enum.KeyCode.P
function library:SetBind(new)
	bind = new 
end
function library:Destroy()
	ScreenGui:Destroy()
end
function library:NewWindow(RezxHub)

	local MainWindow = Instance.new("ImageLabel")
	local Mouse = game.Players.LocalPlayer:GetMouse()
	local Circle = Instance.new("ImageLabel")
	Circle.Name = "Circle"
	Circle.Parent = ScreenGui
	Circle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Circle.BackgroundTransparency = 1
	Circle.ZIndex = 10
	Circle.Image = "http://www.roblox.com/asset/?id=6031625146"
	Circle.ImageColor3 = Color3.fromRGB(255, 255, 255)
	Circle.ImageTransparency = 0.5
	local function CircleClick(Button, X, Y)
		coroutine.resume(coroutine.create(function()
			Button.ClipsDescendants = true
			local Circle = ScreenGui:WaitForChild("Circle"):Clone()
			Circle.Parent = Button
			local NewX = X - Circle.AbsolutePosition.X
			local NewY = Y - Circle.AbsolutePosition.Y
			Circle.Position = UDim2.new(0, NewX, 0, NewY)
			local Size = 0
			if Button.AbsoluteSize.X > Button.AbsoluteSize.Y then
				Size = Button.AbsoluteSize.X * 1.5
			elseif Button.AbsoluteSize.X < Button.AbsoluteSize.Y then
				Size = Button.AbsoluteSize.Y * 1.5
			elseif Button.AbsoluteSize.X == Button.AbsoluteSize.Y then
				Size = Button.AbsoluteSize.X * 1.5
			end
			local Time = 0.5
			tween:Create(Circle,TweenInfo.new(Time,Enum.EasingStyle.Sine),{Size = UDim2.new(0, Size, 0, Size),Position = UDim2.new(0.5, -Size / 2, 0.5, -Size / 2)}):Play()
			for i = 1, 10 do
				Circle.ImageTransparency = Circle.ImageTransparency + 0.05
				wait(Time / 10)
			end
			Circle:Destroy()
		end))
	end
	local Close = Instance.new("ImageButton")
	local SectionTab = Instance.new("Frame")
	local Section_List = Instance.new("UIListLayout")
	local Hub = Instance.new("TextLabel")
	local UICorner_10 = Instance.new("UICorner")
	local Porn = Instance.new("TextLabel")
	local Custom = Instance.new("TextLabel")
	local btnGradient_2 = Instance.new("UIGradient")
	ScreenGui.Parent = game.CoreGui
	MainWindow.Name = "MainWindow"
	MainWindow.Parent = ScreenGui
	MainWindow.AnchorPoint = Vector2.new(0.5, 0.5)
	MainWindow.BackgroundColor3 = Color3.fromRGB(39, 39, 39)
	MainWindow.BackgroundTransparency = 1
	MainWindow.ClipsDescendants = true
	MainWindow.Position = UDim2.new(0.5, 0, 0.5, 0)
	MainWindow.Size = UDim2.new(0, 0, 0, 0)
	MainWindow.Image = "rbxassetid://3570695787"
	MainWindow.ImageColor3 = Color3.fromRGB(39, 39, 39)
	MainWindow.ScaleType = Enum.ScaleType.Slice
	MainWindow.SliceCenter = Rect.new(100, 100, 100, 100)
	MainWindow.SliceScale = 0.050
	MainWindow.AnchorPoint = Vector2.new(0.5,0.5)
	local PageFoler = Instance.new("Folder")
	PageFoler.Parent = MainWindow
	PageFoler.Name = 'Pages'
	--<<<  Make Connection 
	tween:Create(MainWindow,TweenInfo.new(0.4,Enum.EasingStyle.Back),{Size = UDim2.new(0, 440, 0, 282)}):Play()
	dragify(MainWindow)
	game:GetService("UserInputService").InputBegan:Connect(function(input)
		if input.KeyCode == bind then 
			if library.toggled == false then
				library.toggled = true  
				tween:Create(MainWindow,TweenInfo.new(0.4,Enum.EasingStyle.Back,Enum.EasingDirection.In),{Size = UDim2.new(0, 0, 0, 0)}):Play()
			else 
				library.toggled = false 
				tween:Create(MainWindow,TweenInfo.new(0.4,Enum.EasingStyle.Back),{Size = UDim2.new(0, 440, 0, 282)}):Play()
			end 
		end
	end)

	-- >>>
	SectionTab.Name = "SectionTab"
	SectionTab.Parent = MainWindow
	SectionTab.BackgroundColor3 = Color3.fromRGB(36, 36, 36)
	SectionTab.BackgroundTransparency = 1
	SectionTab.Position = UDim2.new(0.046052631, 0, 0.142078027, 0)
	SectionTab.Size = UDim2.new(0, 414, 0, 21)
	Section_List.Name = "Section_List"
	Section_List.Parent = SectionTab
	Section_List.FillDirection = Enum.FillDirection.Horizontal
	Section_List.SortOrder = Enum.SortOrder.LayoutOrder
	Section_List.Padding = UDim.new(0, 6)
	Close.Name = "Close"
	Close.Parent = MainWindow
	Close.BackgroundColor3 = maincolor
	Close.BackgroundTransparency = 1
	Close.Position = UDim2.new(0.915366888, 0, 0.0280000009, 0)
	Close.Size = UDim2.new(0, 21, 0, 21)
	Close.Image = "http://www.roblox.com/asset/?id=6031094678"
	Close.ImageColor3 = maincolor
	Close.ScaleType = Enum.ScaleType.Fit
	Close.MouseButton1Click:Connect(function()
		tween:Create(MainWindow,TweenInfo.new(0.2,Enum.EasingStyle.Back,Enum.EasingDirection.In),{Size = UDim2.new(0,0,0,0)}):Play()
		wait(0.3)
		ScreenGui:Destroy()
	end)
	Close.MouseLeave:Connect(function()
		tween:Create(Close,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{ImageColor3 = maincolor}):Play()
	end)
	Close.MouseEnter:Connect(function()
		tween:Create(Close,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{ImageColor3 = Color3.fromRGB(245, 245, 245)}):Play()
	end)
	local UICorner_9 = Instance.new("UICorner")
	
	local function showall()
		for i, v in next,PageFoler[library.currenttab]:GetChildren() do
			if filter(v) then
				v.Visible = true
			end
		end
	end
	
	UICorner_10.CornerRadius = UDim.new(0.150000006, 0)
	UICorner_10.Parent = Hub
	Porn.Name = "Rezx"
	Porn.Parent = MainWindow
	Porn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Porn.BackgroundTransparency = 1
	Porn.Position = UDim2.new(0.04, 0, 0.03, 0)
	Porn.Size = UDim2.new(0, 43, 0, 21)
	Porn.Font = Enum.Font.Sarpanch
	Porn.Text = RezxHub
	Porn.TextColor3 = Color3.fromRGB(255, 255, 255)
	Porn.TextSize = 16.000
	Custom.Name = "Custom"
	Custom.Parent = MainWindow
	Custom.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Custom.BackgroundTransparency = 1
	Custom.Position = UDim2.new(0.044484295, 0, 0.027999986, 0)
	Custom.Size = UDim2.new(0, 102, 0, 21)
	Custom.Visible = false
	Custom.Font = Enum.Font.Sarpanch
	Custom.Text = "REZX HUB"
	Custom.TextColor3 = Color3.fromRGB(255, 255, 255)
	Custom.TextSize = 16.000
	Custom.TextXAlignment = Enum.TextXAlignment.Left
	btnGradient_2.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, maincolor), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(193, 116, 22))}
	btnGradient_2.Rotation = 90
	btnGradient_2.Name = "btnGradient"
	btnGradient_2.Parent = Custom
	local TabHandler = {}
	function TabHandler:NewSection(nam)

		local name = tostring(nam) or tostring(math.random(1,5000))
		local TabFrame = Instance.new("ScrollingFrame")
		local Element_List = Instance.new("UIListLayout")
		local TabName = Instance.new("TextButton")
		local Underline = Instance.new("Frame")
		local base = UDim2.new(0.037083853, 0, 0.269503534, 0)
		TabFrame.Name = name 
		TabFrame.Parent = PageFoler
		TabFrame.Active = true
		TabFrame.BackgroundColor3 = Color3.fromRGB(39, 39, 39)
		TabFrame.BorderSizePixel = 0
		TabFrame.Position = base
		TabFrame.Size = UDim2.new(0, 412, 0, 200)
		TabFrame.ScrollBarThickness = 0
		TabFrame.Visible = false 
		TabFrame.ClipsDescendants  = true 

		Element_List.Name = "Element_List"
		Element_List.Parent = TabFrame
		Element_List.HorizontalAlignment = Enum.HorizontalAlignment.Center
		Element_List.SortOrder = Enum.SortOrder.LayoutOrder
		Element_List.Padding = UDim.new(0, 3)
		Element_List:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
			local absoluteSize = Element_List.AbsoluteContentSize
			TabFrame.CanvasSize = UDim2.new(0, absoluteSize.X, 0, absoluteSize.Y)
		end)
		TabName.Name = name .. ": Tab"
		TabName.Parent = SectionTab
		TabName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		TabName.BackgroundTransparency = 1
		TabName.Size = UDim2.new(0, 49, 0, 21)
		TabName.Font = Enum.Font.Sarpanch
		TabName.Text = name
		TabName.TextColor3 = Color3.fromRGB(150,150,150)
		TabName.TextSize = 14.000

		Underline.Name = "Underline"
		Underline.Parent = TabName
		Underline.BackgroundColor3 = maincolor
		Underline.Position = UDim2.new(0, 0, 0.952380955, 0)
		Underline.Size = UDim2.new(0, 0, 0, 1)
		Underline.Visible = true 
		Underline.BorderSizePixel  = 0
		Underline.AnchorPoint = Vector2.new(0,0)
		if firstpage == '' then
			wait(0.4)
			firstpage = name 
			tween:Create(Underline,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{Size = UDim2.new(0, 49, 0, 1)}):Play()
			tween:Create(TabName,TweenInfo.new(0.3,Enum.EasingStyle.Sine),{TextColor3 = Color3.fromRGB(255,255,255)}):Play()
			TabFrame.Visible = true 
			TabFrame.Position = base + UDim2.new(-1, 0, 0, 0)
			local tween = game.TweenService:Create(TabFrame, TweenInfo.new(0.2, Enum.EasingStyle.Sine, Enum.EasingDirection.In), {
				Position = base
			})
			tween:Play()
		end
		TabName.MouseButton1Click:Connect(function()
			for i,v in pairs(PageFoler:GetChildren()) do 
				if v.Visible == true then 
					local tween = game.TweenService:Create(v, TweenInfo.new(0.2, Enum.EasingStyle.Linear, Enum.EasingDirection.Out), {
						Position = base + UDim2.new(1, 0, 0, 0),
					})
					tween:Play()
					tween.Completed:Wait()
					v.Visible = false 
				end 
			end
			for i,v in pairs(SectionTab:GetChildren()) do
				if v.Name:find("Tab") then 
					tween:Create(v.Underline,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{Size = UDim2.new(0, 0, 0, 1)}):Play()
					tween:Create(v,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{TextColor3 = Color3.fromRGB(150,150,150)}):Play()						
					library.currenttab = tostring(name)
					local a = math.random(1,5)
				end
			end
			tween:Create(Underline,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{Size = UDim2.new(0, 49, 0, 1)}):Play()
			tween:Create(TabName,TweenInfo.new(0.3,Enum.EasingStyle.Sine),{TextColor3 = Color3.fromRGB(255,255,255)}):Play()
			for i,v in pairs(PageFoler:GetChildren()) do 
				if v.Name == name then 
					v.Visible = true 
					v.Position = base + UDim2.new(-1, 0, 0, 0)
					local tween = game.TweenService:Create(v, TweenInfo.new(0.2, Enum.EasingStyle.Linear, Enum.EasingDirection.In), {
						Position = base
					})
					tween:Play()
				end
			end
		end)
		local Element = {}
		function Element:Bind(nam,ke,callbackontyp,callbac)
			if typeof(callbac) ~= 'function' then warn("Element:Bind() need 4 arguments (<str> name,<enum> key,<boolean> callbackwhenconfirm,<function> callback) ") end 
			local callbackontype = callbackontyp or false
			local name = tostring(nam) or "Keybind"
			local key = ke or Enum.KeyCode.F
			local callback = callbac or function() end
			local name = tostring(nam) or tostring(math.random(1,5000))
			local keyname = tostring(key.Name)
			local NewBind = Instance.new("TextButton")
			local Bind = Instance.new("TextButton")
			NewBind.Name = "NewBind"
			NewBind.Parent = TabFrame
			NewBind.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			NewBind.BackgroundTransparency = 1
			NewBind.Position = UDim2.new(0.0606796145, 0, -0.0673758835, 0)
			NewBind.Size = UDim2.new(0, 404, 0, 21)
			NewBind.Font = Enum.Font.Sarpanch
			NewBind.Text = name
			NewBind.TextColor3 = Color3.fromRGB(200, 200, 200)
			NewBind.TextSize = 14.000
			NewBind.TextWrapped = true
			NewBind.TextXAlignment = Enum.TextXAlignment.Left
			Bind.Name = "Bind"
			Bind.Font = Enum.Font.Sarpanch
			Bind.Parent = NewBind
			Bind.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Bind.BackgroundTransparency = 1
			Bind.BorderSizePixel = 0
			Bind.Position = UDim2.new(0.938, 0,-0.095, 0)
			Bind.Size = UDim2.new(0, 25, 0, 25)
			Bind.Text = keyname
			Bind.TextSize = 16
			Bind.TextColor3 = Color3.fromRGB(255,255,255)
			local tog = false 
			local function fadeon()
				tween:Create(Bind,TweenInfo.new(0.2),{TextColor3 = Color3.fromRGB(255, 255, 255)}):Play()
				tween:Create(NewBind,TweenInfo.new(0.2),{TextColor3 = Color3.fromRGB(255,255,255)}):Play()
			end
			local function fadeoff()
				tween:Create(Bind,TweenInfo.new(0.2),{TextColor3 = maincolor}):Play()
				tween:Create(NewBind,TweenInfo.new(0.2),{TextColor3 = Color3.fromRGB(200, 200, 200)}):Play()
			end
			local function Bind1()
				Bind.Text = "..."
				local uis = game:GetService("UserInputService").InputBegan:wait()
				if uis.KeyCode.Name ~= "Unknown" and uis.UserInputType  == Enum.UserInputType.Keyboard then
					Bind.Text =  uis.KeyCode.Name
					key = uis.KeyCode
				end
				if callbackontype then
					callback(key)
				end
			end
			if  not callbackontype  then 
				game:GetService("UserInputService").InputBegan:connect(function(current, pressed)
					if not pressed then
						if current.KeyCode.Name == key.Name then
							callback(key)
						end
					end
				end)
			end 
			NewBind.MouseEnter:Connect(fadeon)
			NewBind.MouseLeave:Connect(fadeoff)
			Bind.MouseButton1Click:Connect(Bind1)
			NewBind.MouseButton1Click:Connect(Bind1)
		end
		function Element:Button(name,callback)
			local NewButton = Instance.new("TextButton")
			local btnRound = Instance.new("UICorner")
			NewButton.Name = "NewButton"
			NewButton.Parent = TabFrame
			NewButton.BackgroundColor3 = Color3.fromRGB(48,48,48)
			NewButton.BorderSizePixel = 0
			NewButton.Position = UDim2.new(0.144532919, 0, 0.00531914877, 0)
			NewButton.Size = UDim2.new(0, 404, 0, 21)
			NewButton.AutoButtonColor = false
			NewButton.Font = Enum.Font.Sarpanch
			NewButton.Text = name 
			NewButton.TextColor3 = Color3.fromRGB(200,200,200)
			NewButton.TextSize = 14.000
			NewButton.Visible = true
			NewButton.ZIndex = 1
			btnRound.CornerRadius = UDim.new(0.12, 0)
			btnRound.Name = "btnRound"
			btnRound.Parent = NewButton
			local BtnIcon = Instance.new("ImageButton")
			BtnIcon.Name = "BtnIcon"
			BtnIcon.Parent = NewButton
			BtnIcon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			BtnIcon.BackgroundTransparency = 1
			BtnIcon.BorderSizePixel = 0
			BtnIcon.Position = UDim2.new(0.9455, 0,0.05, 0)
			BtnIcon.Size = UDim2.new(0, 19, 0, 19)
			BtnIcon.AutoButtonColor = false
			BtnIcon.ImageColor3 = Color3.fromRGB(200,200,200)
			BtnIcon.ZIndex = 5
			local function fadeon()
				tween:Create(NewButton,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{BackgroundColor3 = Color3.fromRGB(70,70,70),TextColor3 = Color3.fromRGB(255,255,255)}):Play()
				tween:Create(BtnIcon,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{ImageColor3 = Color3.fromRGB(255,255,255)}):Play()

			end
			local function fadeoff()
				tween:Create(NewButton,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{BackgroundColor3 = Color3.fromRGB(48,48,48),TextColor3 = Color3.fromRGB(200,200,200)}):Play()
				tween:Create(BtnIcon,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{ImageColor3 = Color3.fromRGB(200,200,200)}):Play()	
			end
			NewButton.MouseEnter:Connect(fadeon)
			NewButton.MouseLeave:Connect(fadeoff)
			NewButton.MouseButton1Click:Connect(function()
				CircleClick(NewButton, Mouse.X, Mouse.Y)
				callback()
			end)
			BtnIcon.MouseButton1Click:Connect(function()
				CircleClick(NewButton, Mouse.X, Mouse.Y)
				callback()
			end)
		end
	
		function Element:Slider(nam,mi,ma,callbac)
			local name = nam or 'Slider'
			local min = mi or 1 

			local max = ma or 10
			local callback = callbac or function() end 
			local NewSlider = Instance.new("TextLabel")
			local SliderBackground = Instance.new("Frame")

			local SliderRound = Instance.new("UICorner")
			local Slide = Instance.new("ImageButton")
			local Des = Instance.new("TextLabel")


			NewSlider.Name = "NewSlider"
			NewSlider.Parent = TabFrame
			NewSlider.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			NewSlider.BackgroundTransparency = 1
			NewSlider.Position = UDim2.new(0.0606796145, 0, -0.0673758835, 0)
			NewSlider.Size = UDim2.new(0, 404, 0, 21)
			NewSlider.Font = Enum.Font.Sarpanch
			NewSlider.Text = name
			NewSlider.TextColor3 = Color3.fromRGB(200, 200, 200)
			NewSlider.TextSize = 14.000
			NewSlider.TextWrapped = true
			NewSlider.TextXAlignment = Enum.TextXAlignment.Left

			SliderBackground.Name = "SliderBackground"
			SliderBackground.Parent = NewSlider
			SliderBackground.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
			SliderBackground.Position = UDim2.new(0.725247502, 0, 0.380952388, 0)
			SliderBackground.Size = UDim2.new(0, 95, 0, 4)


			SliderRound.CornerRadius = UDim.new(0.5, 0)
			SliderRound.Name = "SliderRound"
			SliderRound.Parent = SliderBackground

			Slide.Name = "Slide"
			Slide.Parent = SliderBackground
			Slide.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Slide.BackgroundTransparency = 1
			Slide.Position = UDim2.new(-7.4505806e-09, 0, -1.75, 0)
			Slide.Size = UDim2.new(0, 18, 0, 18)
			Slide.Image = "http://www.roblox.com/asset/?id=6031625146"
			Slide.ImageColor3 = maincolor

			Des.Name = "Des"
			Des.Parent = NewSlider
			Des.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Des.BackgroundTransparency = 1
			Des.Position = UDim2.new(0.520, 0, -0.067, 0)
			Des.Size = UDim2.new(0, 55, 0, 21)
			Des.Font = Enum.Font.Sarpanch
			Des.Text = min..'/'..max
			Des.TextColor3 = Color3.fromRGB(200, 200, 200)
			Des.TextSize = 14.000
			Des.TextWrapped = true
			Des.AutomaticSize = Enum.AutomaticSize.X
			Des.TextXAlignment = Enum.TextXAlignment.Right
			local down = false 

			local function fadeon()
				tween:Create(NewSlider,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{TextColor3 = Color3.fromRGB(255,255,255)}):Play()
				tween:Create(Des,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{TextColor3 = Color3.fromRGB(255,255,255)}):Play()
			end
			local function fadeoff()
				if down then return end 
				tween:Create(NewSlider,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{TextColor3 = Color3.fromRGB(200,200,200)}):Play()
				tween:Create(Des,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{TextColor3 = Color3.fromRGB(200,200,200)}):Play()

			end
			Des.MouseEnter:Connect(fadeon)
			NewSlider.MouseEnter:Connect(fadeon)
			Des.MouseLeave:Connect(fadeoff)
			NewSlider.MouseLeave:Connect(fadeoff)

			Slide.MouseButton1Down:connect(function()
				down = true
				fadeon()
				while down and game:GetService('RunService').RenderStepped:wait() do
					local percentage = math.clamp(((Mouse.X  - SliderBackground.AbsolutePosition.X) / (SliderBackground.AbsoluteSize.X)), 0,1)

					Slide:TweenPosition(UDim2.new(percentage - 0.1, 0, -1.75, 0), Enum.EasingDirection.InOut, Enum.EasingStyle.Linear, 0.05)
					tween:Create(Slide,TweenInfo.new(0.2),{Size = UDim2.new(0, 18, 0, 18),ImageColor3 = Color3.fromRGB(255,255,255)}):Play()
					-- tween:Create(SliderBackground2,TweenInfo.new(0.05,Enum.EasingStyle.Sine),{Size = UDim2.new(SliderBackground.Size.X, 0, 4)}):Play()

					local value = (percentage * (max - min)) + min
					Des.Text = string.format("%d/%d", value, max)
					spawn(function()
						callback(value)
					end)
				end
			end)
			game:GetService("UserInputService").InputEnded:Connect(function(input)
				if input.UserInputType == Enum.UserInputType.MouseButton1 and down == true  then
					down = false
					wait()
					tween:Create(Slide,TweenInfo.new(0.2),{ImageColor3 = maincolor}):Play()


					fadeoff()
				end 
			end)

		end
		function Element:Drop(nam,lis,cb)
			local dropfunc = {}
			local name = tostring(nam) or math.random(1,5000)
			local list = lis or {}
			local callback = cb or function() end 
			local DropdownToggle = Instance.new("TextButton")
			local DropRound = Instance.new("UICorner")
			local DropToggleIcon = Instance.new("ImageButton")
			local DropRefresh = Instance.new("ImageButton")
			local DropList = Instance.new("ScrollingFrame")
			local DropListLayout = Instance.new("UIListLayout")
			local DropListRound = Instance.new("UICorner")
			DropdownToggle.Name = "DropdownToggle"
			DropdownToggle.Parent = TabFrame
			DropdownToggle.BackgroundColor3 = maincolor
			DropdownToggle.BorderSizePixel = 0
			DropdownToggle.Position = UDim2.new(-0.00239206385, 0, 0.0443262421, 0)
			DropdownToggle.Size = UDim2.new(0, 404, 0, 21)
			DropdownToggle.ZIndex = 5
			DropdownToggle.AutoButtonColor = false
			DropdownToggle.Font = Enum.Font.Sarpanch
			DropdownToggle.Text = name 
			DropdownToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
			DropdownToggle.TextSize = 14.000
			DropRound.CornerRadius = UDim.new(0.150000006, 0)
			DropRound.Name = "DropRound"
			DropRound.Parent = DropdownToggle
			DropToggleIcon.Name = "DropToggleIcon"
			DropToggleIcon.Parent = DropdownToggle
			DropToggleIcon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropToggleIcon.BackgroundTransparency = 1
			DropToggleIcon.BorderSizePixel = 0
			DropToggleIcon.Position = UDim2.new(0.938118815, 0, -0.095238097, 0)
			DropToggleIcon.Size = UDim2.new(0, 25, 0, 25)
			DropToggleIcon.AutoButtonColor = false
			DropToggleIcon.Image = "http://www.roblox.com/asset/?id=6034818372"
			DropToggleIcon.ImageColor3 = Color3.fromRGB(0, 0, 0)
			DropToggleIcon.ZIndex = 5


			DropRefresh.Name = "DropdownRefreshButton"
			DropRefresh.Parent = DropdownToggle
			DropRefresh.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			DropRefresh.BackgroundTransparency = 1
			DropRefresh.BorderSizePixel = 0
			DropRefresh.Position = UDim2.new(0.89, 0, -0.095238097, 0)
			DropRefresh.Size = UDim2.new(0, 23, 0, 23)
			DropRefresh.AutoButtonColor = false
			DropRefresh.Image = "http://www.roblox.com/asset/?id=6031097226"
			DropRefresh.ImageColor3 = Color3.fromRGB(0, 0, 0)
			DropRefresh.ZIndex = 5
			DropRefresh.Visible = false 
			DropRefresh.ImageTransparency  = 1
			DropList.Name = "DropList"
			DropList.Parent = TabFrame
			DropList.Active = true
			DropList.BackgroundColor3 = Color3.fromRGB(21, 21, 21)
			DropList.BorderSizePixel = 0
			DropList.Position = UDim2.new(0, 0, 1.16215849, 0)
			DropList.Size = UDim2.new(0, 404, 0, 0)
			DropList.Visible = false
			DropList.ZIndex = 1
			DropList.ScrollBarThickness = 2
			DropListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
				local absoluteSize = DropListLayout.AbsoluteContentSize
				DropList.CanvasSize = UDim2.new(0, absoluteSize.X, 0, absoluteSize.Y)
			end)
			DropListLayout.Name = "DropListLayout"
			DropListLayout.Parent = DropList
			DropListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
			DropListLayout.SortOrder = Enum.SortOrder.LayoutOrder
			DropListLayout.Padding = UDim.new(0,2)
			DropListRound.CornerRadius = UDim.new(0.150000006, 0)
			DropListRound.Name = "DropListRound"
			DropListRound.Parent = DropList
			local tog = false
			local function Close()
				tog = false
				tween:Create(DropToggleIcon,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{Rotation  = 0,ImageColor3 = Color3.fromRGB(0, 0, 0) }):Play()
				tween:Create(DropList,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{
					Size = UDim2.new(0, 404, 0, 0)
				}):Play()
				wait(0.2)
				DropList.Visible = false
			end
			local function Check()
				CircleClick(DropdownToggle, Mouse.X, Mouse.Y)
				if tog == false then 
					tween:Create(DropRefresh,TweenInfo.new(0.1,Enum.EasingStyle.Sine),{ImageTransparency  = 1}):Play()
					tog = true 

					tween:Create(DropToggleIcon,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{Rotation  = 180 ,ImageColor3 = Color3.fromRGB(50,50,50)}):Play()
					DropList.Visible = true 
					tween:Create(DropList,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{
						Size = UDim2.new(0, 404, 0, 56)
					}):Play()
				else 
					Close()
					tween:Create(DropRefresh,TweenInfo.new(0.1,Enum.EasingStyle.Sine),{ImageTransparency  = 0}):Play()
				end
			end
			local function add(v)
				local DropListBtn = Instance.new("TextButton")
				local UICorner = Instance.new("UICorner")
				DropListBtn.Name = "DropListBtn"
				DropListBtn.Parent = DropList
				DropListBtn.BackgroundColor3 = Color3.fromRGB(50,50,50)
				DropListBtn.Size = UDim2.new(0, 398,0, 17)
				DropListBtn.ZIndex = 1
				DropListBtn.AutoButtonColor = false
				DropListBtn.Font = Enum.Font.Sarpanch
				DropListBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
				DropListBtn.TextSize = 12.000
				DropListBtn.Text = tostring(v)
				UICorner.CornerRadius = UDim.new(0.150000006, 0)
				UICorner.Parent = DropListBtn
				DropListBtn.MouseButton1Click:Connect(function()
					callback(tostring(v))
					Close()
				end)
				local function fadeon()
					tween:Create(DropListBtn,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{BackgroundColor3 = Color3.fromRGB(50,50,50)}):Play()
				end
				local function fadeoff()
					tween:Create(DropListBtn,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{BackgroundColor3 = Color3.fromRGB(50,50,50)}):Play()
				end
				DropListBtn.MouseEnter:Connect(fadeon)
				DropListBtn.MouseLeave:Connect(fadeoff)
			end
			local function clearlist()
				for i,v in next,DropList:GetChildren() do 
					if v:IsA("TextButton") then 
						v:Destroy()
					end
				end
			end
			local function refresh(list)
				clearlist()
				for i,v in next,list do 
					add(v)
				end
			end
			for i,v in pairs(list) do 
				add(v)
			end
			local old = DropToggleIcon.Position
			local function fadeon()
				if tog then return end
				tween:Create(DropRefresh,TweenInfo.new(0.1,Enum.EasingStyle.Sine),{ImageTransparency  = 0}):Play()
				for i=1,2 do 
					tween:Create(DropToggleIcon,TweenInfo.new(0.1,Enum.EasingStyle.Sine),{Position = old + UDim2.new(0,0,0.2,0)}):Play()
					wait(0.1)
					tween:Create(DropToggleIcon,TweenInfo.new(0.1,Enum.EasingStyle.Sine),{Position = old}):Play()
					wait(0.1)
				end 
			end
			local function fadeoff()
				tween:Create(DropRefresh,TweenInfo.new(0.1,Enum.EasingStyle.Sine),{ImageTransparency  = 1}):Play()
				--	tween:Create(DropdownToggle,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{BackgroundColor3 = maincolor}):Play()
			end
			DropdownToggle.MouseEnter:Connect(fadeon)
			DropdownToggle.MouseLeave:Connect(fadeoff)
			DropdownToggle.MouseButton1Click:Connect(Check)
			DropToggleIcon.MouseButton1Click:Connect(Check)
			-- Addition function
			function dropfunc:Clear()
				clearlist()
			end
			function dropfunc:Add(a)
				add(tostring(a))
			end
			function dropfunc:Remove(a)
				for i,v in next,DropList:GetChildren() do 
					if v:IsA("TextButton") and v.Text == tostring(a) then 
						v:Destroy()
					end
				end
			end
			function dropfunc:Refresh(list)
				refresh(list)
			end
			function dropfunc:on(path)
				DropRefresh.Visible = true 
				DropRefresh.MouseButton1Click:Connect(function()
					tween:Create(DropRefresh,TweenInfo.new(0.5,Enum.EasingStyle.Sine),{Rotation = DropRefresh.Rotation +  180 * 4}):Play()
					if  tostring(typeof(path)) == 'table' then 
						refresh(path)
					else 
						clearlist()
						for i,v in next,path:GetChildren() do
							add(v.Name)
						end
					end
				end)
			end
			return dropfunc
		end
		function  Element:h1(text,hidetext)
			local hide = hidetext or false  
			local h1Holder = Instance.new("Frame")
			local Line = Instance.new("Frame")
			local H1Text = Instance.new("TextLabel")

			h1Holder.Name = text
			h1Holder.Parent = TabFrame
			h1Holder.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			h1Holder.BackgroundTransparency = 1.000
			h1Holder.Position = UDim2.new(0.0339805819, 0, 0.589999974, 0)
			h1Holder.Size = UDim2.new(0, 384, 0, 33)

			Line.Name = "Line"
			Line.Parent = h1Holder
			Line.BackgroundColor3 = maincolor
			Line.BorderSizePixel = 0
			Line.Position = UDim2.new(-0.0504904948, 0, 0.436788619, 0)
			Line.Size = UDim2.new(0, 421, 0, 2)

			H1Text.Name = "H1Text"
			H1Text.Parent = Line
			H1Text.BackgroundColor3 = Color3.fromRGB(39, 39, 39)
			H1Text.Position = UDim2.new(0.39, 0,-4.833, 0)
			H1Text.Size = UDim2.new(0, 103, 0, 20)
			H1Text.Font = Enum.Font.Sarpanch
			H1Text.Text = text or 'H1'
			H1Text.Visible = not hide 
			H1Text.BorderSizePixel = 0 
			H1Text.TextColor3 = Color3.fromRGB(150,150,150)
			H1Text.TextScaled = true
			H1Text.TextSize = 16.000
			H1Text.TextWrapped = true
		end
		function Element:Box(nam,callbac)
			local boxfunc = {}
			local name = tostring(nam) or"Box"
			local callback = callbac or function() end 
			local name = tostring(nam) or tostring(math.random(1,5000))
			local NewBox = Instance.new("TextButton")
			local Box = Instance.new("TextBox")
			local Hover = Instance.new("ImageLabel")		NewBox.Name = "NewBox"
			local Underline = Instance.new("Frame")
			Underline.Name = "Underline"
			Underline.Parent = Box
			Underline.BackgroundColor3 = maincolor
			Underline.Position = UDim2.new(0, 0, 0.952380955, 0)
			Underline.Size = UDim2.new(0, 0, 0, 1)
			Underline.Visible = true 
			Underline.AnchorPoint = Vector2.new(0,0)
			Underline.BorderSizePixel = 0
			NewBox.Parent = TabFrame
			NewBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			NewBox.BackgroundTransparency = 1
			NewBox.Position = UDim2.new(0.0606796145, 0, -0.0673758835, 0)
			NewBox.Size = UDim2.new(0, 404, 0, 21)
			NewBox.Font = Enum.Font.Sarpanch
			NewBox.Text = name
			NewBox.TextColor3 = Color3.fromRGB(200, 200, 200)
			NewBox.TextSize = 14.000
			NewBox.TextWrapped = true
			NewBox.TextXAlignment = Enum.TextXAlignment.Left
			Box.Name = "Box"
			Box.Font = Enum.Font.Arial
			Box.Parent = NewBox
			Box.BackgroundColor3 = Color3.fromRGB(54, 54, 54)
			Box.BorderSizePixel = 0
			Box.Position = UDim2.new(0.552, 0,0.048, 0)
			Box.Size = UDim2.new(0, 181,0, 20)
			Box.PlaceholderText = 'Text'
			Box.PlaceholderColor3  = Color3.fromRGB(90,90,90)
			Box.TextSize = 14
			Box.TextColor3 = Color3.fromRGB(255,255,255)
			Box.Text = ''
			local tog = false 
			local function fadeon()
				--	tween:Create(Box,TweenInfo.new(0.2),{ImageColor3 = Color3.fromRGB(255, 255, 255)}):Play()
				tween:Create(NewBox,TweenInfo.new(0.2),{TextColor3 = Color3.fromRGB(255,255,255)}):Play()
			end
			local function fadeoff()
				--	tween:Create(Box,TweenInfo.new(0.2),{ImageColor3 = maincolor}):Play()	if not tog then 
				if not tog then 
					tween:Create(NewBox,TweenInfo.new(0.2),{TextColor3 = Color3.fromRGB(200, 200, 200)}):Play()
				end 
			end
			Box.MouseEnter:Connect(fadeon)
			Box.MouseLeave:Connect(fadeoff)
			NewBox.MouseEnter:Connect(fadeon)
			NewBox.MouseLeave:Connect(fadeoff)
			Box.Focused:Connect(function()
				tween:Create(Underline,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{Size = UDim2.new(0, 181, 0, 1) }):Play()
				tog = true 
				fadeon()
			end)
			Box.FocusLost:Connect(function()
				tween:Create(Underline,TweenInfo.new(0.2,Enum.EasingStyle.Sine),{Size = UDim2.new(0, 0, 0, 1) }):Play()
				tog = false 
				fadeoff()
				callback(tostring(Box.Text))
			end)
			-- Additional Function 
			function  boxfunc:Refresh(new)
				Box.Text = new 
			end
			return boxfunc  
		end
		function  Element:Text(tex,ico)
			local vis = (ico ~= nil and true) or false 
			local icon = vis and tostring(ico) or ''
			local textfunc = {}
			local text = tex or 'TextValue'
			local NewText = Instance.new("TextLabel")
			local ImageLabel = Instance.new("ImageLabel")

			NewText.Name = "TextA"
			NewText.Parent = TabFrame
			NewText.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			NewText.BackgroundTransparency = 1
			NewText.Position = UDim2.new(0.00364077673, 0, 0.109999999, 0)
			NewText.Size = UDim2.new(0, 409, 0, 30)
			NewText.Font = (vis and Enum.Font.Sarpanch) or  Enum.Font.Sarpanch
			NewText.Text = text 
			NewText.TextColor3 =  Color3.fromRGB(255, 255, 255)
			NewText.TextSize = 18.000



			ImageLabel.Parent = NewText
			ImageLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			ImageLabel.BackgroundTransparency = 1.000
			ImageLabel.Position = UDim2.new(0.0366748162, 0, 0.100000009, 0)
			ImageLabel.Size = UDim2.new(0, 23, 0, 23)
			ImageLabel.Image = icon
			ImageLabel.Visible = vis 

			-- Additional Function 
			function  textfunc:Refresh(new,ico1)
				local vis1 = (ico1 ~= nil and true) or false 
				local icon1 = vis and tostring(ico1) or ''

				NewText.Text = new 
				ImageLabel.Image  =( vis1 and icon1) or icon 
			end
			return textfunc  
		end
		function Element:Toggle(nam,callback)
			local togfunc = {}
			local name = tostring(nam) or tostring(math.random(1,5000))
			local NewToggle = Instance.new("TextButton")
			local Toggle = Instance.new("ImageButton")
			local Hover = Instance.new("ImageLabel")		NewToggle.Name = "NewToggle"
			NewToggle.Parent = TabFrame
			NewToggle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			NewToggle.BackgroundTransparency = 1
			NewToggle.Position = UDim2.new(0.0606796145, 0, -0.0673758835, 0)
			NewToggle.Size = UDim2.new(0, 404, 0, 21)
			NewToggle.Font = Enum.Font.Sarpanch
			NewToggle.Text = name
			NewToggle.TextColor3 = Color3.fromRGB(200, 200, 200)
			NewToggle.TextSize = 14.000
			NewToggle.TextWrapped = true
			NewToggle.TextXAlignment = Enum.TextXAlignment.Left
			Toggle.Name = "Toggle"
			Toggle.Parent = NewToggle
			Toggle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Toggle.BackgroundTransparency = 1
			Toggle.BorderSizePixel = 0
			Toggle.Position = UDim2.new(0.938118815, 0, -0.095238097, 0)
			Toggle.Size = UDim2.new(0, 25, 0, 25)
			Toggle.AutoButtonColor = false
			Toggle.Image = "http://www.roblox.com/asset/?id=6031068420"
			Toggle.ImageColor3 = maincolor
			Toggle.ImageTransparency  = 0 
			local tog = false 
			local function fadeon()
				tween:Create(Toggle,TweenInfo.new(0.2),{ImageColor3 = Color3.fromRGB(255, 255, 255)}):Play()
				tween:Create(NewToggle,TweenInfo.new(0.2),{TextColor3 = Color3.fromRGB(255,255,255)}):Play()
			end
			local function fadeoff()
				tween:Create(Toggle,TweenInfo.new(0.2),{ImageColor3 = maincolor}):Play()
				tween:Create(NewToggle,TweenInfo.new(0.2),{TextColor3 = Color3.fromRGB(200, 200, 200)}):Play()
			end
			print(typeof(callback),"<")
			local function toggle()
				tween:Create(Toggle,TweenInfo.new(0.1,Enum.EasingStyle.Sine),{ImageTransparency  = 1 }):Play()
				wait(0.1) 
				if tog == false then 
					tog = true 
					Toggle.Image = 'http://www.roblox.com/asset/?id=6031068421'
				else 
					tog = false 
					Toggle.Image = "http://www.roblox.com/asset/?id=6031068420"
				end
				tween:Create(Toggle,TweenInfo.new(0.1,Enum.EasingStyle.Sine),{ImageTransparency  = 0 }):Play()

				callback(tog)

			end
			Toggle.MouseEnter:Connect(fadeon)
			Toggle.MouseLeave:Connect(fadeoff)
			NewToggle.MouseEnter:Connect(fadeon)
			NewToggle.MouseLeave:Connect(fadeoff)
			Toggle.MouseButton1Click:Connect(toggle)
			NewToggle.MouseButton1Click:Connect(toggle) 
			
			-- Additional Function 
			function togfunc:Set(a)
				Toggle.Image = (a == true and "http://www.roblox.com/asset/?id=6031068421" or "http://www.roblox.com/asset/?id=6031068420" )
				tog = a  

				callback(tog)

			end
			return togfunc 
		end
		return Element
	end
	return TabHandler
end
return library
