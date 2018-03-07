---
layout: base
permalink: /note/2017-03-07-00
title: cocoapods引起的AppIcon不显示的bug
---

Xcode 9之后公司主APP的图片显示不出来了

查了一下是执行[CP] Copy Pods Resources这一步时候出的问题

这个东西是cocoapods执行install或者update之后加到工程里的

内容是执行一个shell脚本

在这个shell脚本的最后有这么一段

    if [[ -n "${WRAPPER_EXTENSION}" ]] && [ "`xcrun --find actool`" ] && [ -n "$XCASSET_FILES" ]
    then
      # Find all other xcassets (this unfortunately includes those of path pods and other targets).
      OTHER_XCASSETS=$(find "$PWD" -iname "*.xcassets" -type d)
      while read line; do
        if [[ $line != "${PODS_ROOT}*" ]]; then
          XCASSET_FILES+=("$line")
        fi
      done <<<"$OTHER_XCASSETS"

      printf "%s\0" "${XCASSET_FILES[@]}" | xargs -0 xcrun actool --output-format human-readable-text --notices --warnings --platform "${PLATFORM_NAME}" --minimum-deployment-target "${!DEPLOYMENT_TARGET_SETTING_NAME}" ${TARGET_DEVICE_ARGS} --compress-pngs --compile "${BUILT_PRODUCTS_DIR}/${UNLOCALIZED_RESOURCES_FOLDER_PATH}"
    fi

在满足三个条件的时候会执行这段代码

0. 有WRAPPER_EXTENSION这个变量 (值就是app)

1. xcrun支持actool (actool是用来合并xcasset的官方工具)

2. 某一个pod包含了xcasset

目的是将主工程的xcasset和Pod的xcasset一起利用actool合成car

我猜测的原因是Xcode 9之后在执行打包car的时候添加了--app-icon参数

所以这块重写之后有问题

解决办法就是也添加上--app-icon参数

    post_install do |installer|
        copy_pods_resources_path = "Pods/Target Support Files/Pods-IconTest/Pods-IconTest-resources.sh"
        string_to_replace = '--compile "${BUILT_PRODUCTS_DIR}/${UNLOCALIZED_RESOURCES_FOLDER_PATH}"'
        assets_compile_with_app_icon_arguments = '--compile "${BUILT_PRODUCTS_DIR}/${UNLOCALIZED_RESOURCES_FOLDER_PATH}" --app-icon "${ASSETCATALOG_COMPILER_APPICON_NAME}" --output-partial-info-plist "${BUILD_DIR}/assetcatalog_generated_info.plist"'
        text = File.read(copy_pods_resources_path)
        new_contents = text.gsub(string_to_replace, assets_compile_with_app_icon_arguments)
        File.open(copy_pods_resources_path, "w") {|file| file.puts new_contents }
    end
