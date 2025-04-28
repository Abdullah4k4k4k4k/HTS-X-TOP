--[[
    HTS X Hub - سكربت هب عالمي يعمل على جميع منافذ روبلوكس وبيئات التنفيذ
    الميزات:
    - واجهة متجاوبة تعمل على جميع أحجام الشاشات
    - دعم لكافة المنافذ (PC, Mobile, Console)
    - دعم لجميع البيئات التنفيذية (KRNL, Delta X, Aruss X, Synapse X)
    - تصميم فخم مع شعار HTS X
    - وظائف متقدمة تعمل في جميع الألعاب
]]

local HTSX = {}

-- تحديد نوع المنفذ التابع للمستخدم
HTSX.Platform = (function()
    if UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled then
        return "Mobile"
    elseif UserInputService.GamepadEnabled and not UserInputService.KeyboardEnabled then
        return "Console"
    else
        return "PC"
    end
end)()

-- تحديد البيئة التنفيذية
HTSX.Executor = (function()
    if syn and syn.request then
        return "Synapse X"
    elseif krnl and krnl.request then
        return "KRNL"
    elseif secure_load then
        return "Delta X"
    elseif Aruss then
        return "Aruss X"
    else
        return "Unknown"
    end
end)()

-- إعدادات الواجهة المتجاوبة
HTSX.ResponsiveSettings = {
    FontSizes = {
        PC = 18,
        Mobile = 22,
        Console = 20
    },
    WindowSizes = {
        PC = {Width = 500, Height = 650},
        Mobile = {Width = 400, Height = 700},
        Console = {Width = 450, Height = 600}
    },
    ButtonHeights = {
        PC = 30,
        Mobile = 40,
        Console = 35
    }
}

-- مكتبات متوافقة مع جميع المنافذ والبيئات
local Rayfield
local success, err = pcall(function()
    Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/shlexware/Rayfield/main/source'))()
end)

if not success then
    -- حل بديل في حالة فشل تحميل Rayfield
    Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/shlexware/Rayfield/main/source', true))()
end

local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local GuiService = game:GetService("GuiService")

-- وظائف التحقق من المنفذ والبيئة
function HTSX:IsMobile()
    return self.Platform == "Mobile"
end

function HTSX:IsConsole()
    return self.Platform == "Console"
end

function HTSX:IsPC()
    return self.Platform == "PC"
end

function HTSX:IsSupportedExecutor()
    local supported = {"Synapse X", "KRNL", "Delta X", "Aruss X"}
    for _, v in pairs(supported) do
        if self.Executor == v then
            return true
        end
    end
    return false
end

-- وظائف التكيف مع الشاشة
function HTSX:GetScreenInfo()
    local viewportSize = workspace.CurrentCamera.ViewportSize
    local isPortrait = viewportSize.Y > viewportSize.X
    return {
        Width = viewportSize.X,
        Height = viewportSize.Y,
        AspectRatio = viewportSize.X / viewportSize.Y,
        IsPortrait = isPortrait
    }
end

function HTSX:AdaptValue(values)
    if self:IsMobile() then
        return values.Mobile or values.Default
    elseif self:IsConsole() then
        return values.Console or values.Default
    else
        return values.PC or values.Default
    end
end

-- تهيئة الواجهة المتجاوبة مع دعم جميع البيئات
function HTSX:InitResponsiveUI()
    -- التحقق من دعم البيئة
    if not self:IsSupportedExecutor() then
        warn("HTS X Hub - البيئة التنفيذية غير معتمدة بالكامل: " .. self.Executor)
    end

    local screenInfo = self:GetScreenInfo()
    local isSmallScreen = screenInfo.Width < 1000
    
    -- ضبط أحجام الخطوط
    local baseFontSize = self:AdaptValue({
        PC = isSmallScreen and 16 or 18,
        Mobile = 20,
        Console = 18,
        Default = 16
    })
    
    -- ضبط أحجام النوافذ
    local windowWidth = math.min(self:AdaptValue({
        PC = 500,
        Mobile = screenInfo.Width * 0.9,
        Console = 450,
        Default = 400
    }), screenInfo.Width * 0.95)
    
    local windowHeight = math.min(self:AdaptValue({
        PC = 650,
        Mobile = screenInfo.Height * 0.8,
        Console = 600,
        Default = 550
    }), screenInfo.Height * 0.9)
    
    -- إنشاء نافذة متجاوبة مع تعديلات للتوافق
    local success, window = pcall(function()
        return Rayfield:CreateWindow({
            Name = "HTS X Hub | " .. game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name,
            LoadingTitle = "جاري تحميل HTS X Hub...",
            LoadingSubtitle = "إصدار عالمي | منفذ: " .. self.Platform .. " | بيئة: " .. self.Executor,
            ConfigurationSaving = {
                Enabled = true,
                FolderName = "HTSXConfig",
                FileName = "HTSX_" .. game.PlaceId
            },
            Discord = {
                Enabled = true,
                Invite = "https://discord.gg/htsx",
                RememberJoins = true
            },
            KeySystem = false,
        })
    end)
    
    if not success then
        -- حل بديل لإنشاء النافذة في حالة فشل الطريقة الأولى
        self.Window = Rayfield:CreateWindow({
            Name = "HTS X Hub | " .. game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name,
            LoadingTitle = "جاري تحميل HTS X Hub...",
            LoadingSubtitle = "إصدار عالمي | منفذ: " .. self.Platform,
            ConfigurationSaving = {
                Enabled = false
            }
        })
    else
        self.Window = window
    end
    
    -- ضبط حجم النافذة
    self.Window:SetSize(UDim2.new(0, windowWidth, 0, windowHeight))
    
    -- إنشاء تبويبات رئيسية
    self:CreateMainTab()
    self:CreateUniversalTab()
    self:CreatePlayerTab()
    self:CreateTeleportTab()
    self:CreateSettingsTab()
    
    -- إضافة استجابة لتغير حجم الشاشة
    workspace.CurrentCamera:GetPropertyChangedSignal("ViewportSize"):Connect(function()
        self:OnScreenResize()
    end)
end

-- وظائف الطيران المعدلة للتوافق مع جميع البيئات
function HTSX:EnableCrossPlatformFly()
    local player = game:GetService("Players").LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")
    
    -- طريقة آمنة لتغيير حالات Humanoid
    pcall(function()
        humanoid:SetStateEnabled(Enum.HumanoidStateType.FallingDown, false)
        humanoid:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, false)
    end)
    
    local rootPart = character:FindFirstChild("HumanoidRootPart")
    if not rootPart then return end
    
    -- إنشاء الأجزاء الفيزيائية بطريقة متوافقة
    local bodyGyro = Instance.new("BodyGyro")
    bodyGyro.P = 10000
    bodyGyro.maxTorque = Vector3.new(100000, 100000, 100000)
    bodyGyro.cframe = rootPart.CFrame
    
    local bodyVelocity = Instance.new("BodyVelocity")
    bodyVelocity.velocity = Vector3.new(0, 0, 0)
    bodyVelocity.maxForce = Vector3.new(100000, 100000, 100000)
    
    -- طريقة آمنة لإضافة الأجزاء إلى الشخصية
    pcall(function()
        bodyGyro.Parent = rootPart
        bodyVelocity.Parent = rootPart
    end)
    
    local flySpeed = 50
    local flyUp = false
    local flyDown = false
    
    -- نظام تحكم متعدد المنافذ والبيئات
    if self:IsMobile() then
        -- عناصر تحكم للهاتف
        local flyControls = self:CreateMobileFlyControls()
        
        flyControls.UpButton.MouseButton1Down:Connect(function()
            flyUp = true
        end)
        
        flyControls.UpButton.MouseButton1Up:Connect(function()
            flyUp = false
        end)
        
        flyControls.DownButton.MouseButton1Down:Connect(function()
            flyDown = true
        end)
        
        flyControls.DownButton.MouseButton1Up:Connect(function()
            flyDown = false
        end)
    else
        -- تحكم لوحة المفاتيح/الجيم باد
        local inputBegan = UserInputService.InputBegan:Connect(function(input, gameProcessed)
            if gameProcessed then return end
            
            if input.KeyCode == Enum.KeyCode.Space then
                flyUp = true
            elseif input.KeyCode == Enum.KeyCode.LeftShift then
                flyDown = true
            end
        end)
        
        local inputEnded = UserInputService.InputEnded:Connect(function(input, gameProcessed)
            if gameProcessed then return end
            
            if input.KeyCode == Enum.KeyCode.Space then
                flyUp = false
            elseif input.KeyCode == Enum.KeyCode.LeftShift then
                flyDown = false
            end
        end)
        
        table.insert(self.Connections, inputBegan)
        table.insert(self.Connections, inputEnded)
    end
    
    local heartbeat = RunService.Heartbeat:Connect(function()
        if not bodyGyro or not bodyVelocity then return end
        
        local camera = workspace.CurrentCamera
        local rootPart = character:FindFirstChild("HumanoidRootPart")
        if not rootPart then return end
        
        -- التحكم في الارتفاع
        local verticalVelocity = 0
        if flyUp then
            verticalVelocity = flySpeed
        elseif flyDown then
            verticalVelocity = -flySpeed
        end
        
        -- التحكم في الاتجاه (يعمل بشكل مختلف حسب المنفذ)
        local direction = Vector3.new(0, 0, 0)
        
        if self:IsMobile() then
            -- تحكم اللمس للهاتف
            for _, touch in pairs(UserInputService:GetTouches()) do
                if touch.UserInputType == Enum.UserInputType.Touch then
                    local touchPos = touch.Position
                    local screenCenter = Vector2.new(screenInfo.Width/2, screenInfo.Height/2)
                    
                    if touchPos.X < screenCenter.X - 100 then
                        direction = direction - camera.CFrame.RightVector
                    elseif touchPos.X > screenCenter.X + 100 then
                        direction = direction + camera.CFrame.RightVector
                    end
                    
                    if touchPos.Y < screenCenter.Y - 100 then
                        direction = direction + camera.CFrame.LookVector
                    elseif touchPos.Y > screenCenter.Y + 100 then
                        direction = direction - camera.CFrame.LookVector
                    end
                end
            end
        else
            -- تحكم لوحة المفاتيح/الجيم باد
            if UserInputService:IsKeyDown(Enum.KeyCode.W) then
                direction = direction + camera.CFrame.LookVector
            end
            if UserInputService:IsKeyDown(Enum.KeyCode.S) then
                direction = direction - camera.CFrame.LookVector
            end
            if UserInputService:IsKeyDown(Enum.KeyCode.D) then
                direction = direction + camera.CFrame.RightVector
            end
            if UserInputService:IsKeyDown(Enum.KeyCode.A) then
                direction = direction - camera.CFrame.RightVector
            end
        end
        
        if direction.Magnitude > 0 then
            direction = direction.Unit * flySpeed
            bodyVelocity.velocity = Vector3.new(direction.X, verticalVelocity, direction.Z)
        else
            bodyVelocity.velocity = Vector3.new(0, verticalVelocity, 0)
        end
        
        bodyGyro.cframe = camera.CFrame
    end)
    
    table.insert(self.Connections, heartbeat)
    self.FlyObjects = {bodyGyro, bodyVelocity}
end

-- وظائف مساعدة محسنة للتوافق
function HTSX:ShowNotification(title, content)
    local success, result = pcall(function()
        Rayfield:Notify({
            Title = title,
            Content = content,
            Duration = 3,
            Image = 4483345998
        })
    end)
    
    if not success then
        -- طريقة بديلة للإشعارات
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = title,
            Text = content,
            Duration = 3
        })
    end
end

-- إدارة الاتصالات للتنظيف الآمن
HTSX.Connections = {}

function HTSX:Cleanup()
    -- تنظيف جميع الاتصالات
    for _, connection in ipairs(self.Connections) do
        if connection and typeof(connection) == "RBXScriptConnection" then
            connection:Disconnect()
        end
    end
    self.Connections = {}
    
    -- تنظيف عناصر الطيران
    if self.FlyObjects then
        for _, obj in ipairs(self.FlyObjects) do
            if obj and obj.Parent then
                obj:Destroy()
            end
        end
        self.FlyObjects = nil
    end
    
    -- تنظيف عناصر الهاتف
    if self.MobileControls then
        if self.MobileControls.Gui and self.MobileControls.Gui.Parent then
            self.MobileControls.Gui:Destroy()
        end
        self.MobileControls = nil
    end
end

-- بدء تشغيل الهب مع معالجة الأخطاء
local success, err = pcall(function()
    HTSX:InitResponsiveUI()
    HTSX:ShowNotification("HTS X Hub", "تم تحميل الهب بنجاح! المنفذ: " .. HTSX.Platform .. " | البيئة: " .. HTSX.Executor)
end)

if not success then
    warn("فشل تحميل HTS X Hub: " .. tostring(err))
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = "HTS X Hub - خطأ",
        Text = "فشل التحميل: " .. tostring(err),
        Duration = 5
    })
end

-- التنظيف عند إعادة التحمل
game:GetService("Players").LocalPlayer.CharacterAdded:Connect(function()
    HTSX:Cleanup()
end)

return HTSX
