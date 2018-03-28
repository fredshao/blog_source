---
title: Unity3D生成音频波形图
date: 2018-03-28 23:43:22
tags: 游戏开发
---

```c#
// 传入一个AudioClip 会将AudioClip上挂载的音频文件生成频谱到一张Texture2D上
public static Texture2D BakeAudioWaveform(AudioClip _clip) {
        int resolution = 60;	// 这个值可以控制频谱的密度吧，我也不知道
        int width = 1920;		// 这个是最后生成的Texture2D图片的宽度
        int height = 200;		// 这个是最后生成的Texture2D图片的高度

        resolution = _clip.frequency / resolution;

        float[] samples = new float[_clip.samples * _clip.channels];
        _clip.GetData(samples, 0);

        float[] waveForm = new float[(samples.Length / resolution)];

        float min = 0;
        float max = 0;
        bool inited = false;

        for (int i = 0; i < waveForm.Length; i++) {
            waveForm[i] = 0;

            for (int j = 0; j < resolution; j++) {
                waveForm[i] += Mathf.Abs(samples[(i * resolution) + j]);
            }

            if (!inited) {
                min = waveForm[i];
                max = waveForm[i];
                inited = true;
            } else {
                if (waveForm[i] < min) {
                    min = waveForm[i];
                }

                if (waveForm[i] > max) {
                    max = waveForm[i];
                }
            }
            //waveForm[i] /= resolution;
        }


        Color backgroundColor = Color.black;
        Color waveformColor = Color.green;
        Color[] blank = new Color[width * height];
        Texture2D texture = new Texture2D(width, height);

        for (int i = 0; i < blank.Length; ++i) {
            blank[i] = backgroundColor;
        }

        texture.SetPixels(blank, 0);

        float xScale = (float)width / (float)waveForm.Length;

        int tMid = (int)(height / 2.0f);
        float yScale = 1;

        if (max > tMid) {
            yScale = tMid / max;
        }

        for (int i = 0; i < waveForm.Length; ++i) {
            int x = (int)(i * xScale);
            int yOffset = (int)(waveForm[i] * yScale);
            int startY = tMid - yOffset;
            int endY = tMid + yOffset;

            for (int y = startY; y <= endY; ++y) {
                texture.SetPixel(x, y, waveformColor);
            }
        }

        texture.Apply();
        return texture;
    }
```

生成的波形图如下（只截取了一小部分）

{% asset_img sample_1.png %}