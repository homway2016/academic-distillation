# Statistical Visualization Standards — 统计可视化标准

APA 7.0 图表规范、无障碍调色板、图表类型选择、常见陷阱和代码模板。

---

## APA 7.0 Figure Guidelines

### 一般原则

1. **每个图表必须增加价值** — 用一句话或表格能更好表达的数据不要可视化
2. **图表按首次提及顺序编号**（Figure 1, Figure 2, ...）
3. **每个图表必须在正文中被引用**（"As shown in Figure 1, ..."）
4. **caption 在图表下方**（表格 note 在上方）
5. **图表必须不读正文即可理解** — caption 中包含所有必要上下文

### Caption 格式

```
Figure [N]                          ← Bold, 独立一行
[Descriptive Title]                 ← Italic, sentence case, 下一行
Note. [Explanation if needed]       ← Plain text, 以 "Note." 开头
```

### 字体规格

| Element | Size | Style |
|---------|------|-------|
| Figure label | 10-12 pt | Bold |
| Figure title | 10-12 pt | Italic |
| Axis labels | 8-10 pt | Plain, sentence case |
| Axis tick labels | 8-9 pt | Plain |
| Legend text | 8-9 pt | Plain |
| Annotations | 8 pt | Plain or italic |
| Note text | 8-9 pt | Plain |

### 必需元素

- [ ] Axis labels（双轴，描述性，带单位）
- [ ] Tick marks and tick labels
- [ ] Legend（多组图）
- [ ] Error bars or confidence intervals（均值比较）
- [ ] Scale bars（图像/地图）
- [ ] Caption with Figure number + title
- [ ] Note（如需解释）

---

## 无障碍调色板

### Primary: Viridis（感知均匀）

Best for: continuous/sequential data.

| Index | Hex Code |
|-------|----------|
| 0 | `#440154` |
| 1 | `#46327E` |
| 2 | `#365C8D` |
| 3 | `#277F8E` |
| 4 | `#1FA187` |
| 5 | `#4AC16D` |
| 6 | `#9FDA3A` |
| 7 | `#FDE725` |

### Alternative: Cividis（Deuteranopia/Protanopia 优化）

Best for: 色盲可及性至关重要的出版物。

### Categorical: Tol's Qualitative Palette（最多 8 类）

| Label | Hex Code | Sample Use |
|-------|----------|------------|
| Blue | `#0077BB` | Group 1 / Baseline |
| Cyan | `#33BBEE` | Group 2 |
| Teal | `#009988` | Group 3 |
| Orange | `#EE7733` | Group 4 / Highlight |
| Red | `#CC3311` | Group 5 / Alert |
| Magenta | `#EE3377` | Group 6 |
| Grey | `#BBBBBB` | Reference / NA |
| Black | `#000000` | Outline / Text |

### Diverging: Blue-Red（相关/差异图）

| Negative | Zero | Positive |
|----------|------|----------|
| `#2166AC` | `#F7F7F7` | `#B2182B` |

### 无障碍规则

1. Never rely on color alone — pair with shape, pattern, or label
2. Minimum contrast ratio: 3:1 (WCAG AA for non-text elements)
3. Test with a colorblindness simulator before finalizing
4. When printing in grayscale, patterns or labels must still distinguish groups

---

## Chart Type Decision Tree

| Your Data | Your Question | Recommended Chart | Avoid |
|-----------|--------------|-------------------|-------|
| Categories + values | Compare magnitudes | **Bar chart** | Pie chart |
| Categories + values + groups | Compare across groups | **Grouped bar** or **stacked bar** | 3D bar chart |
| Continuous variable, 1 group | Show distribution | **Histogram** + density curve | |
| Continuous variable, 2-5 groups | Compare distributions | **Boxplot** or **violin plot** | Bar chart of means only |
| Two continuous variables | Show relationship | **Scatter plot** + regression line | |
| Time series (1-5 series) | Show trends | **Line chart** | Bar chart for time series |
| Time series (> 5 series) | Show trends | **Small multiples** | Spaghetti plot |
| Correlation matrix | Show multi-variable relationships | **Heatmap** | Scatter plot matrix (too dense) |
| Effect sizes + CIs (meta) | Summarize meta-analysis | **Forest plot** | Bar chart |
| Effect sizes + SE (meta) | Check publication bias | **Funnel plot** | |
| Concepts + relationships | Map theoretical framework | **Network graph** | |
| Proportions summing to 100% | Show composition | **Stacked bar chart** | Pie chart |
| Geographic data | Show spatial patterns | **Choropleth map** | |

### When NOT to Visualize

- Fewer than 3 data points（用文本或表格）
- 单一百分比或均值（在正文中陈述）
- 需要超过 2 句话解释图表的数据（用表格）
- 与表格中已有数据冗余的可视化

---

## Common Pitfalls

### Critical Errors（Never Do）

| Pitfall | Problem | Fix |
|---------|---------|-----|
| **Pie charts** | 人类对比较角度/面积感知差 | Use bar chart |
| **3D charts** | 透视投影扭曲数值 | Use 2D |
| **Dual y-axes** | 暗示虚假相关；尺度选择任意 | Two separate panels |
| **Rainbow colormap** | 非感知均匀；非色盲安全 | Use viridis/cividis |
| **Truncated y-axis** (without marking) | 夸大微小差异 | Start at 0 or mark break clearly |
| **Missing error bars** | 隐藏不确定性 | Add SE, SD, or 95% CI bars |
| **Chartjunk** (decorative elements) | 降低 data-ink ratio | Remove unnecessary elements |

### Subtle Errors（Easy to Miss）

| Pitfall | Problem | Fix |
|---------|---------|-----|
| Unequal bin widths in histogram | 扭曲频率感知 | Use equal bins |
| Overlapping labels | 打印尺寸下不可读 | Rotate, abbreviate, or reduce categories |
| Too many colors (> 8) | 打印尺寸下不可区分 | Group categories or use facets |
| Legend far from data | Reader must scan back and forth | Place legend inside plot area or use direct labels |
| Aspect ratio distortion | 夸大或缩小趋势 | Use 4:3 default; 16:9 for time series |

---

## Python matplotlib Code Templates

### Template 1: Bar Chart

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams.update({
    'font.family': 'sans-serif',
    'font.sans-serif': ['Arial', 'Helvetica', 'DejaVu Sans'],
    'font.size': 9, 'axes.titlesize': 11, 'axes.labelsize': 10,
    'xtick.labelsize': 8, 'ytick.labelsize': 8, 'legend.fontsize': 8,
    'figure.dpi': 300, 'savefig.dpi': 300, 'savefig.bbox': 'tight',
    'axes.spines.top': False, 'axes.spines.right': False,
})
CB = ['#0077BB', '#33BBEE', '#009988', '#EE7733', '#CC3311', '#EE3377']

categories = ['Group A', 'Group B', 'Group C', 'Group D']
values = [4.2, 3.8, 5.1, 4.5]
errors = [0.3, 0.4, 0.2, 0.5]

fig, ax = plt.subplots(figsize=(6.9, 4.5))
bars = ax.bar(categories, values, yerr=errors, capsize=4,
              color=CB[:len(categories)], edgecolor='black', linewidth=0.5)
ax.set_ylabel('Score (points)')
ax.set_xlabel('Group')
ax.set_ylim(0, max(values) * 1.3)

plt.tight_layout()
plt.savefig('figure_01.pdf', format='pdf')
plt.show()
```

### Template 2: Boxplot

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams.update({
    'font.family': 'sans-serif', 'font.size': 9, 'axes.labelsize': 10,
    'figure.dpi': 300, 'axes.spines.top': False, 'axes.spines.right': False,
})
CB = ['#0077BB', '#33BBEE', '#009988', '#EE7733']

np.random.seed(42)
data = [np.random.normal(loc, 1, 50) for loc in [3.5, 4.0, 3.8, 4.5]]
labels = ['Public', 'Private', 'Technical', 'National']

fig, ax = plt.subplots(figsize=(6.9, 4.5))
bp = ax.boxplot(data, labels=labels, patch_artist=True, widths=0.6,
                medianprops=dict(color='black', linewidth=1.5))
for patch, color in zip(bp['boxes'], CB):
    patch.set_facecolor(color)
    patch.set_alpha(0.7)

ax.set_ylabel('Satisfaction Score (1-5)')
ax.set_xlabel('Institution Type')
plt.tight_layout()
plt.savefig('figure_02.pdf', format='pdf')
plt.show()
```

### Template 3: Line Chart (Trend)

```python
import matplotlib.pyplot as plt

plt.rcParams.update({
    'font.family': 'sans-serif', 'font.size': 9, 'axes.labelsize': 10,
    'figure.dpi': 300, 'axes.spines.top': False, 'axes.spines.right': False,
})
CB = ['#0077BB', '#CC3311', '#009988']

years = [2018, 2019, 2020, 2021, 2022, 2023]
series_a = [72, 75, 68, 71, 78, 82]
series_b = [65, 63, 60, 58, 55, 52]

fig, ax = plt.subplots(figsize=(6.9, 4.5))
ax.plot(years, series_a, 'o-', color=CB[0], label='Public universities', linewidth=1.5, markersize=5)
ax.plot(years, series_b, 's--', color=CB[1], label='Private universities', linewidth=1.5, markersize=5)
ax.set_xlabel('Year')
ax.set_ylabel('Enrollment (thousands)')
ax.legend(frameon=False)
ax.set_xlim(min(years) - 0.5, max(years) + 0.5)

plt.tight_layout()
plt.savefig('figure_03.pdf', format='pdf')
plt.show()
```

### Template 4: Scatter Plot + Regression

```python
import matplotlib.pyplot as plt
import numpy as np
from scipy import stats

plt.rcParams.update({
    'font.family': 'sans-serif', 'font.size': 9, 'axes.labelsize': 10,
    'figure.dpi': 300, 'axes.spines.top': False, 'axes.spines.right': False,
})

np.random.seed(42)
x = np.random.uniform(10, 50, 80)
y = 0.6 * x + np.random.normal(0, 5, 80) + 10

slope, intercept, r, p, se = stats.linregress(x, y)
x_line = np.linspace(min(x), max(x), 100)
y_line = slope * x_line + intercept

fig, ax = plt.subplots(figsize=(6.9, 5.5))
ax.scatter(x, y, color='#0077BB', alpha=0.6, edgecolors='black', linewidth=0.3, s=30)
ax.plot(x_line, y_line, color='#CC3311', linewidth=1.5,
        label=f'y = {slope:.2f}x + {intercept:.2f}, r = {r:.2f}, p < .001')
ax.set_xlabel('Faculty-Student Ratio')
ax.set_ylabel('Student Satisfaction Score')
ax.legend(frameon=False, loc='lower right')

plt.tight_layout()
plt.savefig('figure_04.pdf', format='pdf')
plt.show()
```

### Template 5: Forest Plot (Meta-Analysis)

```python
import matplotlib.pyplot as plt
import numpy as np

plt.rcParams.update({'font.family': 'sans-serif', 'font.size': 9, 'axes.labelsize': 10, 'figure.dpi': 300})

studies = ['Smith (2018)', 'Chen (2019)', 'Johnson (2020)', 'Lee (2021)', 'Garcia (2022)', 'Overall']
effects = [0.35, 0.42, 0.28, 0.51, 0.38, 0.39]
ci_lower = [0.15, 0.22, 0.08, 0.31, 0.18, 0.27]
ci_upper = [0.55, 0.62, 0.48, 0.71, 0.58, 0.51]

fig, ax = plt.subplots(figsize=(6.9, 4.0))
y_pos = np.arange(len(studies))

for i, study in enumerate(studies):
    color = '#CC3311' if study == 'Overall' else '#0077BB'
    marker = 'D' if study == 'Overall' else 'o'
    size = 8 if study == 'Overall' else 6
    ax.errorbar(effects[i], i, xerr=[[effects[i]-ci_lower[i]], [ci_upper[i]-effects[i]]],
                fmt=marker, color=color, markersize=size, capsize=3, linewidth=1.2)

ax.axvline(x=0, color='grey', linestyle='--', linewidth=0.8)
ax.set_yticks(y_pos)
ax.set_yticklabels(studies)
ax.set_xlabel("Effect Size (Cohen's d)")
ax.invert_yaxis()
ax.spines['top'].set_visible(False)
ax.spines['right'].set_visible(False)

plt.tight_layout()
plt.savefig('figure_05.pdf', format='pdf')
plt.show()
```

### Template 6: Correlation Heatmap

```python
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns

plt.rcParams.update({'font.family': 'sans-serif', 'font.size': 9, 'figure.dpi': 300})

labels = ['Teaching', 'Research', 'Service', 'Satisfaction', 'Retention']
corr = np.array([
    [1.00, 0.45, 0.32, 0.67, 0.55],
    [0.45, 1.00, 0.28, 0.38, 0.30],
    [0.32, 0.28, 1.00, 0.41, 0.35],
    [0.67, 0.38, 0.41, 1.00, 0.72],
    [0.55, 0.30, 0.35, 0.72, 1.00],
])

fig, ax = plt.subplots(figsize=(5.5, 5.0))
mask = np.triu(np.ones_like(corr, dtype=bool), k=1)
sns.heatmap(corr, mask=mask, annot=True, fmt='.2f', cmap='RdBu_r',
            center=0, vmin=-1, vmax=1, square=True,
            xticklabels=labels, yticklabels=labels,
            linewidths=0.5, cbar_kws={'shrink': 0.8, 'label': 'r'}, ax=ax)

plt.tight_layout()
plt.savefig('figure_06.pdf', format='pdf')
plt.show()
```

---

## R ggplot2 Code Templates

### Template 1: Bar Chart

```r
library(ggplot2)

theme_apa <- theme_minimal(base_size = 10, base_family = "Arial") +
  theme(
    plot.title = element_text(size = 11, face = "bold", hjust = 0),
    axis.title = element_text(size = 10),
    axis.text = element_text(size = 8),
    legend.title = element_text(size = 9),
    legend.text = element_text(size = 8),
    panel.grid.minor = element_blank(),
    panel.grid.major.x = element_blank(),
    strip.text = element_text(size = 9, face = "bold")
  )
cb_palette <- c("#0077BB", "#33BBEE", "#009988", "#EE7733", "#CC3311", "#EE3377")

df <- data.frame(
  group = c("Group A", "Group B", "Group C", "Group D"),
  value = c(4.2, 3.8, 5.1, 4.5),
  se = c(0.3, 0.4, 0.2, 0.5)
)

ggplot(df, aes(x = group, y = value, fill = group)) +
  geom_col(color = "black", linewidth = 0.3, width = 0.7) +
  geom_errorbar(aes(ymin = value - se, ymax = value + se), width = 0.2) +
  scale_fill_manual(values = cb_palette) +
  labs(x = "Group", y = "Score (points)") +
  theme_apa +
  theme(legend.position = "none") +
  coord_cartesian(ylim = c(0, NA))

ggsave("figure_01.pdf", width = 6.9, height = 4.5, units = "in", dpi = 300)
```

### Template 2: Boxplot

```r
library(ggplot2)

theme_apa <- theme_minimal(base_size = 10, base_family = "Arial") +
  theme(
    axis.title = element_text(size = 10), axis.text = element_text(size = 8),
    panel.grid.minor = element_blank(), panel.grid.major.x = element_blank()
  )
cb_palette <- c("#0077BB", "#33BBEE", "#009988", "#EE7733")

set.seed(42)
df <- data.frame(
  type = rep(c("Public", "Private", "Technical", "National"), each = 50),
  score = c(rnorm(50, 3.5, 1), rnorm(50, 4.0, 1), rnorm(50, 3.8, 1), rnorm(50, 4.5, 1))
)

ggplot(df, aes(x = type, y = score, fill = type)) +
  geom_boxplot(alpha = 0.7, outlier.shape = 21, outlier.size = 1.5) +
  scale_fill_manual(values = cb_palette) +
  labs(x = "Institution Type", y = "Satisfaction Score (1-5)") +
  theme_apa +
  theme(legend.position = "none")

ggsave("figure_02.pdf", width = 6.9, height = 4.5, units = "in", dpi = 300)
```

### Template 3: Line Chart (Trend)

```r
library(ggplot2)

theme_apa <- theme_minimal(base_size = 10, base_family = "Arial") +
  theme(
    axis.title = element_text(size = 10), axis.text = element_text(size = 8),
    legend.text = element_text(size = 8), panel.grid.minor = element_blank()
  )

df <- data.frame(
  year = rep(2018:2023, 2),
  enrollment = c(72, 75, 68, 71, 78, 82, 65, 63, 60, 58, 55, 52),
  type = rep(c("Public", "Private"), each = 6)
)

ggplot(df, aes(x = year, y = enrollment, color = type, shape = type)) +
  geom_line(linewidth = 1) +
  geom_point(size = 2.5) +
  scale_color_manual(values = c("#0077BB", "#CC3311")) +
  labs(x = "Year", y = "Enrollment (thousands)", color = NULL, shape = NULL) +
  theme_apa

ggsave("figure_03.pdf", width = 6.9, height = 4.5, units = "in", dpi = 300)
```

### Template 4: Scatter Plot + Regression

```r
library(ggplot2)

theme_apa <- theme_minimal(base_size = 10, base_family = "Arial") +
  theme(
    axis.title = element_text(size = 10), axis.text = element_text(size = 8),
    panel.grid.minor = element_blank()
  )

set.seed(42)
df <- data.frame(ratio = runif(80, 10, 50))
df$satisfaction <- 0.6 * df$ratio + rnorm(80, 0, 5) + 10

ggplot(df, aes(x = ratio, y = satisfaction)) +
  geom_point(color = "#0077BB", alpha = 0.6, size = 1.5) +
  geom_smooth(method = "lm", color = "#CC3311", se = TRUE, linewidth = 1, fill = "#CC3311", alpha = 0.1) +
  labs(x = "Faculty-Student Ratio", y = "Student Satisfaction Score") +
  theme_apa

ggsave("figure_04.pdf", width = 6.9, height = 5.5, units = "in", dpi = 300)
```

---

## LaTeX Figure Inclusion Template

### Single Figure

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=\columnwidth]{figures/figure_01.pdf}
    \caption{\textit{Comparison of Student Satisfaction Scores Across Three Institution Types.}
    Error bars represent 95\% confidence intervals. $N = 1{,}247$.}
    \label{fig:satisfaction}
\end{figure}
```

### Multi-Panel Figure

```latex
\usepackage{subcaption}  % Required in preamble

\begin{figure}[htbp]
    \centering
    \begin{subfigure}[b]{0.48\textwidth}
        \centering
        \includegraphics[width=\textwidth]{figures/figure_02a.pdf}
        \caption{Public universities}
        \label{fig:dist-public}
    \end{subfigure}
    \hfill
    \begin{subfigure}[b]{0.48\textwidth}
        \centering
        \includegraphics[width=\textwidth]{figures/figure_02b.pdf}
        \caption{Private universities}
        \label{fig:dist-private}
    \end{subfigure}
    \caption{\textit{Distribution of Faculty-Student Ratios by Institution Type.}
    Box plots show median, interquartile range, and outliers.}
    \label{fig:ratio-distribution}
\end{figure}
```
